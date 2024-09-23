Mysql에서 다루는 데이터 묶음의 단위를 Page라고 한다

### Page의 종류
Data Page, [[Index Page]], Undo Log Page가 있다

Data Page는 테이블 데이터들이 저장되는 Page 이다

Index Page는 테이블의 Index 정보를 저장하며, Index값과 Data Page 주소를 가진다
쉽게 말해, 인덱스된 컬럼, 컬럼이 존재하는 Data Page의 주소가 Index Page에 저장되는 것이다.

Undo Log Page는 트랜잭션 격리 수준을 구현하기 위해서 트랜잭션이 수행되기 이전의 데이터를 백업하는 Page이다 
> Transaction Manager System은 Transaction Id와 해당 Transaction의 Undo Log Page를 기록하고 가지고 있다.
### Page의 구성

크게 Header와 Body로 나뉘게 된다
기본적으로 16kb의 크기를 가지며
Header는 Page에 대한 메타 정보를 가지며 다음과 같은 정보들로 이루어져 있다
- Page의 고유 식별자(FIL_PAGE_SPACE/FIL_PAGE_OFFSET)
- Page의 유형(FIL_PAGE_TYPE)
- 이전/다음 페이지의 번호(FIL_PAGE_PREV/FIL_PAGE_NEXT)
- 마지막으로 수정된 LSN(Log Sequence Number)(FIL_PAGE_LSN)

Body는 실제 데이터가 저장되는 영역으로, Page 유형에 따라 구조가 다르다
- Data Page
	- Row of Table 정보들이 저장되며

- Index Page의 경우에는 Index 값, Row of Table의 Page 주소가 저장된다
	
- Undo Log Page의 경우에는 트랜잭션을 수행하기 이전의 원본 데이터, 즉 백업 데이터가 저장된다
