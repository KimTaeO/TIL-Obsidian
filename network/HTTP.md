서버와 클라이언트가 데이터를 주고받기 위한 프로토콜
TCP/IP계층에서 작동하며, Stateless 프로토콜이며, Method, Path, Version, Header, Body로 이루어짐

Stateless란 서버가 클라이언트의 정보를 저장하지 않는 것을 의미한다

### HTTP 메시지 구성

#### Request

시작 줄에는 HTTP Method, 사이트 주소, HTTP 버전으로 이루어져 있다
> 예시 GET http://naver.com HTTP/1.1

두번째 줄부터는 **헤더**라고 하는 요청에 대한 정보를 담는 것들로 Key-Value 쌍으로 이루어져 있다. User-Agent, Upgrade-Insecure-Requests 등이 헤더에 포함되며 헤더의 종류는 매우 많다

헤더를 다 작성하고 난 뒤에 개행을 한번 한 뒤 **본문**을 작성할 수 있는데 이는 요청을 보낼 데이터를 담는 부분이다

HTTPS 사용시 [[TLS]]라는 암호화 프로토콜을 사용하여 통신하여 더 안전한 통신을 보장받을 수 있다
### Response

시작 줄은 HTTP 버전, Status Code 등으로 이루어져 있다

두번째 줄부터는 Request와 동일하게 Key-Value 쌍으로 이루어진 헤더이다

헤더를 다 작성하고 난 뒤에는 브라우저가 요청한 데이터를 담는 부분으로 이루어진다

### HTTP 버전별 차이

#### HTTP/1.0
커넥션 하나당 하나의 요청만 처리가 가능, 비효율적이며 서버 부하도 발생
하나의 요청이 처리되기 전 까지 다른 요청 처리 불가
#### HTTP/1.1

- 지정한 TimeOut 동안에 커넥션을 재사용할 수 있도록 함, 기존 연결에서는 HandShaking 생략
- **Pipelining** : 앞 요청을 기다리지 않고 다음 요청을 보냄으로써 기존 방식 개선
  multiplexing과는 다르다
	문제점 
		HOL(Head Of Line Blocking)
			TCP프로토콜의 특징으로 첫번째 요청이 처리 완료되기까지 다른 요청들은 모두 대기해야함
		Fat Message Headers
			HTTP/1.1에는 많은 헤더가 존재하는데 요청할 때마다 중복된 Header 값을 반복적으로 전송하게 된다. 또한 cookie도 요청할 때마다 포함되어 요청된다. 전송하려는 값보다 헤더가 더 큰 경우가 빈번하게 발생
#### HTTP/2
- HTTP/1.X 버전의 성능 향상에 초점을 맞춤으로써 HTTP/1.X을 대체하는 것이 아닌 확장되는 개념으로 등장하였습니다.
- 구글의 SDPY를 참고하여 HTTP/2를 표준화하였습니다
- 내부에 Binary Framing 계층을 추가하여 보낼 데이터를 이진 데이터로 인코딩 후 Frame 단위로 분할하여 전송한다
	* 파싱 속도 및 전송 속도가 빠르며 오류 발생 가능성이 낮아졌다
	* HTTP/1.X 버전에서 발생한 HOL Blocking이 해결됨

	 병렬로 요청을 보내 처리시킬 수 있는 Multiplexing 기능을 제공한다
	 하나의 TCP 커넥션 안에서 여러 Stream을 전송할 수 있기 때문
	 하지만 TCP 태생적인 HOL Blocking 문제가 존재한다
- HTTP/3
  TCP 태생적인 HOL Blocking 을 해결하기 위해 UDP 기반 프로토콜인 QUIC / HTTP/3이 등장함
  