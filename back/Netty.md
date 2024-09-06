Netty는 서버 및 클라이언트의 네트워크 응용 프로그램을 빠르고 쉽게 개발할 수 있는 NIO 클라이언트 서버 프레임워크이다

기존의 BIO 방식은 클라이언트 하나당 스레드 1개를 사용하여 요청을 처리해야 했다
이는 Context Switching 관련 문제와 데이터를 입출력 할때 무한으로 대기해야 하는 문제가 있었다

이를 해결하기 위해 Java에서는 NIO라는 방법을 제시했으며, 이벤트 통지 API로 논블락 소켓을 등록하여 정보를 확인하는 방식을 사용한다

자바의 Selector에서 입출력을 담당하는 Socket의 집합 상태를 확인
클라이언트 당 스레드를 생성하는게 아닌 필요 시에 스레드에게 통지하는 방식이므로 비동기적임

### Netty Component
NIO 기반의 Netty 프레임워크는 비동기식 이벤트 기반 네트워킹을 지원하기에 기존의 동기 기반 네트워크보다 커넥션 처리량이 뛰어나다

기존의 소켓 통신 프로그래밍은 동기적이고 NIO는 비동기적 통신 방식이다 (추가적으로 이벤트 기반이기도 하다)

이런 Netty의 핵심 컴포넌트로는 Channel, CallBack, Future, Event & Handler, Event Loop, PipeLine이 있다

- Channel : 하나 이상의 입출력 작업을 수행할 수 있는 하드웨어 장치, 파일, 네트워크 소켓이나, 프로그램 컴포넌트와 같은 Open된 Connection을 의미한다

- CallBack : 다른 메서드로 자신에 대한 참조를 제공하는 메서드이다. ChannelHandler 인터페이스로 이벤트를 처리한다

- Future : 작업이 완료될 경우 애플리케이션에게 알려주는 역할을 한다. 비동기 작업의 결과물을 담는 PlaceHolder 역할을 한다

- Event & Handler : 작업의 상태 변화를 알리기 위해 Event를 사용하고 발생한 이벤트를 기준으로 Handler를 통해 트리거한다

- [[Event Loop]] : Multiplexing을 이용하여 여러 채널에서 발생하는 이벤트들을 하나의 스레드로 병행 처리할 수 있다. 

- PipeLine : 이벤트 루프에서 이벤트를 받아 핸들러에게 이벤트를 전달함


https://hbase.tistory.com/116