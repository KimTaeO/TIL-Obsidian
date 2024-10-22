### G1 GC
기존의 GC가 Stop The World가 진행되는 시간을 극단적으로 가져가지 않기 위한 전략이었다면, G1 GC는 Full GC를 최대한 피하여 Stop The World가 진행되는 시간을 단축시키는 전략이다.

**용어**
- Evacuation : 객체의 copy 또는 moving을 뜻한다
- Region : 힙메모리 영역을 고정된 크기로 나눈 것
- Humongous Region : 새로 할당하는 인스턴스가 Region 크기의 절반을 넘어가면, G1 GC에서 관리하며 Humongous Region이 된다
- Available / Unused Reion : 아무것도 할당되어있지 않은 영역
- Collection Set : GC가 수행될 Region들의 집합이다. Collection Set이 JVM에서 차지하는 메모리 비율은 1% 이내이다.
- Remembered Set : Reference를 가진 객체가 어느 Region에 있는지 확인하기 위해 Remembered Set을 사용하며
- Mixed Collection : young/old 영역에 발생하는 GC

Garbage 비중이 높은 heap Region을 중점적으로 collection이 일어난다.
Garbage 비중이 높은 부분에 대한 수집과 압축 작업이 주를 이루기 때문에 Garbage First라는 이름이 붙게 되었다.

JVM힙은 2048개의 Region으로 나뉘며, 옵션을 통해 Region 당 1MB ~ 32MB 사이로 지정할 수 있다.

**수행 방식**
Initial Mark, Root Region Scan, Concurrent Mark, Remark, Clean up, Copy 순서로 수행된다

- Initial Mark : Old Region에 존재하는 객체들이 참조하는 Survivor Region을 찾는다. STW O
- Root Region Scan : 찾은 Survivor Region에 대해 GC 대상 객체를 스캔한다.
- Concurrent Mark : 모든 Region에 대해 스캔 작업을 진행하며, GC 대상 객체가 없는 Region을 이후 단계에서 제외하도록 한다.
- Remark : GC에서 제외될 객체를 최종적으로 식별해낸다. STW O
- Clean up : 미사용 객체 수거를 진행 후, 완전히 비워진 Region을 Freelist에 등록하여 재사용할 수 있도록 한다. STW O
- Copy : Clean up 과정에서 완전히 비워지지 않은 Region의 객체들을 Available Region에 복사하여 Compaction을 수행한다. STW O
> G1 GC는 마킹 작업 시에 SATB(Snapshot at the Beginning)를 사용하여 일시 정지 시점(Snapshot)의 객체에 마킹을 하므로 마킹 도중에 GC 대상이 되더라도 포함되지 않는다.


### ZGC
자바 11에 실험적 기능으로 15에서는 정식으로 추가된 garbage collector이다.

G1 GC와는 다르게 Region이 아닌 zPage라는 단위로 heap 메모리를 구분하며 small, medium, large로 나뉜다. 각 타입별로 들어갈 수 있는 객체의 크기가 다르며(2MB, 32MB, N X 2MB), Large타입의 zPage에 하나의 객체만이 들어갈 수 있다.

보통의 리눅스 x86-64 아키텍쳐에서 프로세스는 가상 메모리 주소를 위해 48비트를 사용해 256TB 대역의 가상 메모리를 사용한다. ZGC는 42bit의 가상 메모리 주소를 사용하고, 42~45번째bit를 GC 처리 시 활용을 위한 **Colored Pointer**로 사용한다.

#### Colored Pointer
종류로는 marked0, marked1, remapped, finalizable이 존재하며 이중 finalizable을 제외한 모든 종류가 GC 사용 시 이용된다. 3개의 가상 주소를 하나의 물리 주소로 매핑하는데 이때 연산을 절약하기 위해 mmap을 수행한다

- marked0
- marked1 : 위의 GC 실행마다 marked0 타입과 번갈아 가며 사용하게 되는데 이는 객체가 이번 GC 주기에 remapped 된것인지 저번 주기에 remapped된 것인지도 판별할 수 있다. 만약에 저번 주기에 remapped 된 객체가 남아있다면 잘못된 객체로 판별되어 slow path로 작업을 수행하게 된다
- remapped : 살아 있는 객체를 새로운 ZPage로 옮기는 일련의 과정이 실행되면, 가리키는 주소도 새로운 주소로 변경해야 되는데 이를 위해 fowarding table을 할당하여 관리하는 상태를 remapped라고 한다.
- finalizable

#### Load Barrier
heap 영역에 참조가 발생하면 객체가 참조할 수 있는 상태인지 확인하기 위해 실행되는 코드이다. G1과는 다르게 참조가 해제될 때 참조 상태를 검사하는 write barrier와 대조된다. 문제가 생기면 slow path라는 과정을 실행한 후 참조를 실행한다.

#### Reclaimed
객체가 remapped 된 후 비어있는 ZPage를 회수하는 과정을 Reclaimed라고 한다.

**수행 방식**
10단계를 거쳐 처리가 되나, 크게 2가지로 묶을 수 있다. 첫번째부터 다섯번째 까지는 **coloring** 여섯번째부터 마지막까지는 **relocation**이라 한다.

coloring은 이전 세대의 GC에서는 marking이라 칭하던 작업이다. relocation은 coloring 작업을 마친 객체를 재배치 하는 작업이다.

- phase 1 : 각 스레드에 존재하는 로컬 변수를 스캔한다. 로컬변수를 GC root라 하며, 이를 모아 GC root set을 만든다. 이때 찾은 객체의 42~45번째 비트에 mapped0와 mapped1을 coloring한다. 이 플래그는 GC 주기마다 번갈아 가며 사용한다.
  
  GC 사이클이 끝나고 살아남은 객체를 새로운 ZPage를 만들어 재배치한다.
  
  GC root 객체에 load barrier를 적용해 살아있다고 판단되는 객체를 mark stack에 넣는다

- phase 2 ~ 4 concurrent mark 
  mark stack 안의 객체를 marking 하거나 remapping을 하는 것이다.
  해당 coloring의 결과로 garbage가 존재하는 Page를 relocation page라 한다.

- phase 5 : soft / week / phantom reference에 대한 처리를 진행한다.
- relocation : coloring으로 식별된 참조가 끊긴 객체를 해제한다. 살아있는 객체는 새로 생성한 ZPage에 옮긴다

- phase 6 : GC에서 식별한 relocation set을 초기화한다.
- phase 8 : relocation set의 Garbage를 제거하고 새로운 ZPage를 생성해 옮긴다.
- phase 9 ~ 10 : phase1에서 생성하였던 ZPage에 살아있는 객체를 옮긴다.