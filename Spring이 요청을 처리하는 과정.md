1. DispatcherServlet이 요청을 받게 된다
2. DispatcherServlet은 HandlerMapping이 해당 요청에 알맞는 Controller가 있는지 확인한다
3. HandlerAdapter가 요청을 처리할 Controller에게 전달한다
4. Controller는 Service에게 비즈니스 로직을 위임 
5. 데이터베이스에서 필요한 데이터를 받아오는 등의 처리 수행
6. 컨트롤러는 DispatcherServlet에게 View 이름을 전달
7. DispatcherServlet은 View 이름을 ViewResolver에게 전달
8. View 를 최종적으로 클라이언트에게 전달함으로써 마무리

![[Pasted image 20240903181201.png]]
