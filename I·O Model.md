애플리케이션이 자신의 디바이스가 아닌 외부의 디바이스와 데이터를 주고받기(Read&Write) 위해서는 필연적으로 OS의 System Call을 호출해야 한다.

![[Pasted image 20240925102941.png]]
Write System Call이 발생할 경우에는 OS 커널은 전송하고자 하는 데이터를 [[Socket]]의 send buffer에 복사한다.

Read System Call이 발생할 경우에는 OS 커널은 수신하고자 하는 데이터를 [[Socket]]의 recevie buffer에 복사한다.

OS DMA(Direct Memory Access)가 Network Card로부터 OS Kernel에 데이터를 복사하고, 인터럽트를 일으켜 프로세스가 해당 데이터를 읽어가거나 외부 디바이스에 데이터를 전송하게 된다.

결국 다른 디바이스간 통신은 OS Kernel의 Socket을 활용하여 이루어지게 된다.

이러한 작업을 통틀어 Network I·O라고 부르며, 애플리케이션 관점에서 이는 두가지로 나뉘게 된다.
바로 Blocking I·O, Non-Blocking I·O이다. 
> 이를 구분하는 기준으로는 애플리케이션을 제어하는 관점에서 호출한 함수의 리턴 여부이다

[[동기 비동기와 블락 논블락의 차이점]]

자바의 JDK 1.3에서 사용되는 Java I·O가 Blocking 모드이다
자바는 JDK 1.4에서 추가된 Java New I·O에서 Non-Blocking을 지원하기 시작했다.

Blocking I/O에서는 TCP 네트워킹에서 I/O 작업을 Blocking하게 처리하기 때문에 소켓 연결 및 처리 
Thread가 실제 일을 하고있지 않음에도 Thread를 점유하게 된다.

이는 자연스레 네트워크 I/O 작업마다 Thread를 할당해야 함을 의미하며, 굉장히 비효율적이다.
이런 문제를 해결하기 위해 Spring과 같은 대부분의 서버 프레임워크들은 Connection Pool을 이용하여 비용을 줄였지만, 연결이 아닌 I/O 작업은 여전히 Blocking이다.
![[Pasted image 20240925111954.png]]


Non-Blocking I/O에도 방식이 있다 Polling 방식과 Push 방식이 존재한다

Polling 방식은 직접 Channel들을 순회하며 읽을 데이터를 확인하지만, Push 방식은 Channel의 상태가 변하게 되면, 이벤트를 만들어 Push하게 되면 Thread는 그때만 작업을 수행할 수 있기 때문에 Push 방식은, Polling 방식에 비해 리소스를 효율적으로 사용할 수 있다.

polling 방식은 지속적으로 데이터를 확인하기 때문에 system call을 지속적으로 호출하므로 비효율적이다.

Push 방식은 하나의 스레드로 여러 개의 작업을 처리할 수 있게 된다. 즉, 하나의 통로를 여러 개가 사용할 수 있다(Multiplexing). Selector가 Channel의 변화를 감지하여 이벤트에 맞는 작업을 처리하는것이다.


![[Pasted image 20240925112002.png]]

![[Pasted image 20240925201055.png]]