Database Storage Engine 또는 Storage Engine은 DBMS가 데이터를 삽입, 삭제, 추출, 업데이트 등의 작업을 진행하는데 사용하는 소프트웨어 컴포넌트이다 

### Engine의 종류
- InnoDB
- MyISAM
- Memory
- Archive
- CSV
- Federated

#### InnoDB
MySQL 5.5 이후부터의 기본 엔진이다

Commit, Rollback 등 충돌을 처리하는 기능을 제공한다.
Transaction을 제공하고 ACID를 지원한다
Row Level Lock을 지원한다
외래키를 지원하며
MVCC/SnapShot Read를 제공한다

시스템 자원을 더 사용하며
MyISAM 파일에 비해 크기가 크다

#### MyISAM
MySQL의 5.5 버전까지 기본 엔진이다

Commit, Rollback 등 충돌을 처리하는 기능을 제공한다.
Table Level Lock을 제공한다.
	갱신 작업시 속도가 느리다.
Transaction을 지원하지 않는다.

Data를 효율적으로 저장한다.
InnoDB에 비해 빠르다.
Select 작업 시 속도가 빨라 읽기 작업이 많은 상황에 적합하다.

#### Memory
HEAP 엔진이라고도 불리며 메모리에 데이터를 저장한다(영속성 보장 X)

- Table-level Lock을 제공한다.
- 모든 데이터를 RAM에 저장한다.
- 트랜잭션을 제공하지 않는다.