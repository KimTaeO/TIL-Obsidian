네티로 작성한 네트워크 애플리케이션의 동작 방식과 환경을 설정하는 도우미 클래스이다

설정할 수 있는 요소로는 다음과 같은 요소가 있다

-  전송 계층(소켓 모드 및 I/O 종류)
- 이벤트 루프(단일 스레드,다중 스레드)
- 채널 파이프라인 설정
- 소켓 주소와 포트
- 소켓 옵션

BootStrap을 담당하는 클래스로는 BootStrap, ServerBootStrap가 있으며 모두 AbstractBootStrap 클래스를 상속받는다. ServerBootStrap은 서버 애플리케이션을 만들 때 사용되며, BootStrap은 클라이언트 애플리케이션을 만들 때 주로 사용된다. 차이점으로는 클라이언트 연결 요청을 받을 포트를 바인딩하는 메서드인 bind() 메서드의 유무 차이이다.

ServerBootStrap 클래스를 사용해 설정 가능하며, 해당 클래스는 빌더 패턴으로 이루어져 있다

모든 이벤트를 핸들링하고 I/O 이벤트를 처리할 이벤트 루프 그룹을 설정한다 부모 이벤트 그룹과, 자식 이벤트 그룹이 같음
group(EventLoopGroup group)

첫번째 인수는 부모 이벤트 루프를 설정하고, 모든 이벤트를 핸들링하는 역할이며, 두번째 인수는 자식 이벤트 루프를 설정하고 I/O 이벤트만을 처리하는 역할이다
group(EventLoopGroup group, EventLoopGroup group)

부모 이벤트 루프 그룹이 사용할 네트워크 소켓 입출력 모드를 지정할 수 있다.
Channel 인터페이스를 구현하는 클래스를 인수로 넘길 수 있다. ServerBootStrap의 경우에는 ServerChannel 인터페이스를 구현하는 클래스를 인수로 넘길 수 있다.
C extends Channel
channel(Class\<? extends C\> channelClass)

ChannelHandler를 구현한 클래스를 인수로 넘길 수 있으며, 서버 소켓 채널에서 발생하는 이벤트를 수신하여 처리할 수 있다.
handler(ChannelHadler channelHandler)

handler 메서드와 마찬가지로 ChannelHandler를 구현한 클래스를 인수로 넘길 수 있으며, 클라이언트 소켓 채널에서 발생하는 이벤트를 수신하여 처리할 수 있다.
childHandler(ChannelHadler channelHandler)

소켓의 동작 방식을 지정하기 위한 소켓 옵션을 설정할 수 있다. 애플리케이션의 값을 바꾸는 것이 아닌 커널에서 사용되는 값을 바꾸는 것임에 주의하자. 주로 사용되는 소켓 옵션은 다음과 같다
- TCP_NODELAY : 데이터 송수신에 Nagle 알고리즘의 비활성화 여부를 지정한다. 기본값 false
- SO_KEEPALIVE : 운영체제에서 지정된 시간에 한번씩 keepalive 패킷을 상대방에게 전송한다. 기본값false
- SO_SNDBUF : 상대방에게 송신할 커널 송신 버퍼의 크기 (커널 설정에 의존)
- SO_RCEBUF : 상대방으로부터 수신할 커널 수신 버퍼의 크기 (커널 설정에 의존)
- SO_REUSEADDR :TIME_WAIT 상태의 포트를 서버 소켓에 바인드할 수 있게 한다. 기본값 false
- SO_LINGER : 소켓을 닫을 때 커널의 송신 버퍼에 전송되지 않은 데이터의 전송 대기시간을 지정한다. 기본값 false
- SO_BACKLOG : 동시에 수용 가능한 소켓 연결 수, 동시에 받아들일 수 있는 3 way handshake 요청 시 SYN-RECEIVED된 소켓 연결을 가지고 있는 큐의 크기를 설정한다

서버 소켓 채널의 옵션을 설정한다
option(ChannelOption\<T\> option, T value)

서버에 접속한 클라이언트 소켓 채널의 옵션을 설정한다
childOption(ChannelOption\<T\> option, T value)