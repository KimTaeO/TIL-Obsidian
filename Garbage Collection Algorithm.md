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