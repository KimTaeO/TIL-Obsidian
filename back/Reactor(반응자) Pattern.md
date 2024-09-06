동시성을 다루는 디자인 패턴 중 하나로, 동시에 들어오는 여러 클라이언트의 요청들을 처리하는 기법이다.
- 순차적으로 처리
- 싱글스레드 채택

## 구성요소
* Reactor
	* 싱글 스레드로 이루어져 있으며 무한 반복문을 실행해 이벤트가 발생하면 핸들러에게 이벤트를 디스패치 한다
* Handler
	* Reactor에게 이벤트를 받아 비즈니스 로직을 수행한다

# Reactive Stream
non-blocking, back pressure를 사용한 비동기적인 스트림 처리를 제공하는 표준

> Back Pressure(배압) : 리액티브 스트림은 비동기 처리가 기본적이기 때문에 역압력 기법이 자동으로 탑재되어 `빠른 발행자(Publisher) - 느린 구독자(Subscriber)` 문제를 해결할 수 있음. 즉, Subscriber가 처리할 수 있는 만큼만의 데이터를 Subscriber가 요청하면 전달하는 방식 Dynamic Pull 이라고도 함

Observer, Iterator, 함수형 패러다임을 포함하고 있다

Reactive Stream 시퀀스를 만드는 방법 3가지의 차이점
	just : 시퀀스를 즉시 생성한다
	fromSupplier :  `Supplier<? extends T> supplier`를 인자로 받는다. 인자가 리액티브 스트림을 반환하지 않을 때 사용하면 된다.
	defer : `Supplier<? extends Mono<? extends T>> supplier`를 인자로 받는다. 인자가 리액티브 스트림을 반환할 때 사용하면 된다.

리액티브 스트림을 구독하는 법

Disposable 인터페이스의 subscribe()를 사용하여 Mono\<T\> 와 Flux\<T\>를 구독할 수 있다