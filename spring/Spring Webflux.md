Reactive Programming 방식을 통해 이벤트 기반의 비동기식 애플리케이션을 구축할 수 있다
[[동기 비동기와 블락 논블락의 차이점]]

Reactive Programming을 구현한 Reactor 라이브러리를 사용하여 Reative Stream을 처리한다
[[Reactor(반응자) Pattern]]

### Netty
비동기식 이벤트 기반 서버를 만들 때 사용이 된다
이벤트-기반
비동기 처리
다수의 동시 접속자 처리 가능
HTTP, WebSocket, TCP 다수의 프로토콜 지원
다양한 애플리케이션에 사용 가능한 높은 확장성

Blocking Request
	클라이언트가 요청을 보내면 응답을 받을 때 까지 대기하는 것을 의미한다.
Non-Blocking Request
	요청을 보내고 응답을 받을 때까지 대기하는 것이 아닌 다른 작업을 수행할 수 있다

## Multi Event Loop
단일 스레드로 동작하는 이벤트 루프를 여러 개 사용하는 것을 의미한다. 블로킹 I/O 작업이 일어나더라도 다른 이벤트 루프를 이용하여 멈추지 않고 작업을 수행할 수 있다.

## WebClient
비동기적인 방식으로 HTTP 요청을 보내고 응답을 받을 수 있는 라이브러리이며, Reactive Streams를 이용하여 높은 성능의 네트워크 통신을 구현할 수 있다