데이터베이스의 인덱스 페이지는 다음과 같은 구조로 이루어져 있다
  
모든 인덱스 페이지는 전체적으로 해당 구조를 따른다
  
![[Pasted image 20240923102050.png]]
**FIL Header/ Trailer**
모든 페이지에 포함되는 전형적이고 일반적인 요소입니다. 인덱스 페이지의 독특한 점은 FIL 헤더의 이전페이지와 다음 페이지의 포인터는 같은 레벨에 있는 페이지를 가리킵니다. 그리고 이것은 오름차순으로 정렬된 인덱스 키에 기반한다.

**Index Header**
인덱스 페이지와 레코드 관리에 관련한 많은 필드를 포함한다.

**FSEG Header**
인덱스의 루트 페이지의 FSEG 헤더는 해당 인덱스에 의해 사용되는 파일 세그먼트의 포인터를 포함하고 있다. 모든 다른 인덱스 페이지는 사용되지 않고, 아무것도 채워지지 않는다.

**System Records**
InnoDB는 2가지의 시스템 레코드를 가지고 있는데 각각의 페이지는 infimum, supremum이라고 불린다. 이러한 레코드는 바이트 오프셋에 기반한 페이지를 항상 직접적으로 찾을 수 있도록 하기 위해서 페이지의 고정된 위치에 저장된다.

**User Records**
실질적인 데이터이다 모든 레코드는 다양한 폭의 헤더와 실질적 컬럼 데이터를 스스로 가집니다. 헤더는 페이지 내부의 오름차순으로 정렬된 다음 레코드의 오프셋을 저장하고 있는포인터를 가지고 있으며 단독으로 이루어진 연결 리스트의 형태를 띄고 있다.

**Page Directory**
페이지 디렉토리는 FIL Trailer에서 페이지가 시작하는 가장 위쪽으로 점점 커지며, 페이지의 몇몇 레코드의 포인터를 가지고 있다. (모든 4번째와 8번째 레코드)


### Index Header
Index Header는 다음과 같은 구조로 이루어져 있다
![[Pasted image 20240923104939.png]]
**Index ID**
이 페이지가 속해 있는 Index의 ID를 가지고 있습니다.

**Format Flag**
"Number of Heap Records" 필드보다 상위 비트에 저장됩니다. COMPACT, REDUNDANT 두가지 값이 허용됩니다.

**Maximum Transaction ID**
해당 페이지의 어떠한 기록이나 수정 사항의 최대 Transaction ID 입니다.

**Number of Heap Records**
이 페이지에 있는 총 레코드 수입니다. infimum, supremum과 같은 시스템 레코드, 또한 garbage(삭제된) 레코드의 개수도 포함합니다.

**Number of Records**
이 페이지의 삭제되지 않은 유저 레코드의 수 입니다.

**Heap Top Position**
현재 사용된 공간의 마지막 바이트 오프셋 입니다.
모든 공간은 Heap Top과 페이지 디렉토리의 마지막은 빈 공간입니다.

**First Garbage Record Offset**
garbage(삭제된) 레코드 리스트의 첫번째 엔트리 포인터를 가지고 있습니다. 이 리스트는 각각의 레코드 헤더에 다음 레코드 포인터를 가지고 있습니다(연결 리스트 형태, InnoDB에서는 이것을 free라고 부르지만, 무언가 혼란스러운 부분이 있습니다)

**Garbage Space**
Garbage Record 리스트가 차지하고 있는 바이트 합계를 나타냅니다

**Last Insert Position**
페이지에 삽입된 레코드의 바이트 오프셋을 나타냅니다

**Page Direction**
3가지 값이 대표적으로 Page Direction에서 사용됩니다 LEFT, RIGHT, NO_DIRECTION
이 값은 해당 페이지가 순차적인 삽입을 시도하고 있는지를 나타낸다.(LEFT : 적은 값부터 삽입, RIGHT : 큰 값부터 삽입, NO_DIRECTION : 랜덤한 삽입) 데이터 삽입 시마다, 데이터 삽입 위치를 결정하기 위해서 마지막 삽입 위치의 키와 현재 삽입된 레코드 키를 비교합니다.

**Number of Inserts in Page Direction**
Page Direction이 설정되면, 모든 삽입은 방향을 리셋하지 않는다. 대신에 이 값을 증가시킨다

**Number of Directory Slots**
16 바이트의 오프셋을 가진 페이지 디렉토리의 크기를 나타내는 Slot을 나타낸다

**Page Level**
인덱스에서의 이 페이지의 레벨을 담고 있다 Leaf Page라면 레벨이 0 이고, B+Tree의 위쪽으로 갈수록 레벨이 높아진다