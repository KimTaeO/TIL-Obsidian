JavaScript는 싱글 스레드 언어이다. 이는 한번에 하나의 일만 수행할 수 있다는 뜻이며, 
Memory Heap과 Call Stack으로 이루어져 있다

Memory Heap은 데이터를 임시 저장하는 곳으로 함수나 변수, 함수를 사용할 때 사용하는 값들을 저장합니다

Call Stack은 코드가 실행되면 코드의 내부 실행 순서를 기록해 놓고 하나하나씩 차례대로 실행시킨다.
	**순차적으로 코드를 실행시킬 수 있도록 도와줌**
	web API, Callback Queue, event loop를 사용하여 오래걸리는 작업에 대해 관리

## JS Engine의 동작 과정



결과적으로 event loop는 Call Stack **비어있는지를 주기적으로 확인하여** Callback Queue에서 Callback function을 가져와 Call Stack에서 Javascript 코드가 실행될 수 있도록 돕는 역할을 합니다. event loop가 반복적으로 Call Stack이 비어있는지 확인 하는 것을 tick이라고 합니다.