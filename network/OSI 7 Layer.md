네트워킹 전반의 동작을 설명하는 모델이다

* 표준화를 통하여 장비별로 이질적인 포트나 프로토콜 문제를 해결한다
* 복잡한 네트워크를 부분으로 나누어 쉽게 이해하고 설계와 개발을 편하게 하기 위함
* 계층번호에 ```L```을 붙여 표기하기도 한다

# 계층의 구조

7계층 Application
6계층 Presentation
5계층 Session
4계층 Transport
3계층 Network
2계층 Data Link
1계층 Physical

> 각 N 계층은 N+1 계층에게 서비스를 제공한다
> 각 N 계층은 N-1 계층의 서비스를 이용한다

L1에서 L7로 갈수록 추상화 수준이 높으며, 소프트웨어를 많이 다룬다

### Protocol(프로토콜)
* 동일 계층에서의 논리적/물리적 장비 간의 통신
* 같은 계층의 다른 장비간의 통신
	* 수평적 통신이라고도 한다
* 프로토콜끼리 주고 받는 메시지는 PDU(Protocol Data Unit)라고 한다
	* 각 PDU는 해당하는 프로토콜의 스펙을 구현한 포맷을 갖는다

### Interface
* 동일 장비의 위아래 인접 계층 간에 이동하는 정보를 나타냄
* 동일 장비의 N 계층과 N+1 계층, N계층과 N-1 계층간의 통신을 다룬다

![[OSI 7 Layer.png]]
프로토콜 간의 통신이 일어난다고 가정할 때 Host A의 7 계층에서 Host B의 7 계층으로 데이터를 전송한다고 가정하면 실제 메시지는 
Host A의 {7 -> 6 -> 5 -> 4 -> 3 -> 2 -> 1} -> Host B의 {1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7}
다음과 같은 과정을 거쳐 전달된다

어떠한 메시지도 물리 계층을 통하지 않고서는 다른 장비로 전달할 수 없다

