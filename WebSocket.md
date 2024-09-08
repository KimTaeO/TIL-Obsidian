WebSocket 양방향 통신을 위한 프로토콜이다. HTTP 프로토콜(HTTP는 TCP 프로토콜 위에서 동작) 위에서 동작 가능하며 방화벽 규칙 또한 재사용할 수 있다

일반 HTTP 요청에 Upgrade 헤더를 포함한 request를 전송하면 WebSocket 프로토콜로 변환한다
Upgrade헤더가 포함된 요청을 받은 서버는 101 Status Code를 반환하게 된다.

일반적으로 TCP 프로토콜에서 동작하기 때문에 HTTP와 같이 HandShake 과정을 통해 연결을 수립하고 해제한다

### WebSocket 통신 헤더

#### Request
- Upgrade : 프로토콜을 전환하기 위한 헤더. value에 websocket이라는 값이 들어가며 들어가있지 않다면 cross-protocol attack이라고 간주하여 웹 소켓 접속을 중단시킨다.
- Connection : 현재의 전송이 완료된 후 소켓 접속을 유지할 것인지에 대한 정보. value에 Upgrade 값이 들어가며 들어가지 않는다면 웹 소켓 접속을 중단시킨다.
- Sec-WebSocket-Key : 유효한 요청인지 확인하기 위해서 사용하는 키이다.
- Sec-WebSocket-Protocol : 사용하고자 하는 하나 이상의 웹 소켓 프로토콜을 지정하기 위해 사용한다(선택적으로 필요한 경우에만 사용한다)
- Sec-WebSocket-Version : 클라이언트가 사용하고자 하는 웹 소켓 프로토콜의 버전이다.
- Origin : CORS 정책으로 인해 만들어진 헤더이다 Cross-Site Websocket Hijacking과 같은 공격을 피하기 위함이다.

#### Response
- Sec-WebSocket-Accept : 요청 헤더의 Sec-WebSocket-Key에 Unique한 아이디를 더해서 SHA-1로 해싱 후 Base64로 인코딩한 값이 들어간다. 웹 소켓 연결이 수립되었음을 알리는 헤더이기도 하다.


### WebSocket 통신
연결이 수립되면 서로 데이터를 주고받는데 통신 시에는 메시지라는 단위로 데이터를 주고받으며, 이 메시지는 Frame(프레임)이 모여 구성된다.

프레임은 small header + payload로 구성된다

참고
https://alnova2.tistory.com/915

https://doozi0316.tistory.com/entry/WebSocket%EC%9D%B4%EB%9E%80-%EA%B0%9C%EB%85%90%EA%B3%BC-%EB%8F%99%EC%9E%91-%EA%B3%BC%EC%A0%95-socketio-Polling-Streaming
