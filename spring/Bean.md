IoC 방식으로 관리하는 오브젝트. 즉 스프링 컨테이너(Bean Factory)가 관리하는 객체를 Bean이라고 한다

Singleton 패턴으로 편하게 재사용할 수 있고 어디서든 불러서 사용할 수 있도록 한다

#### Bean 등록 방법
- Component Scanning
	@Component 어노테이션이 작성된 클래스를 @SpringBootApplication에서 해당 어노테이션이 붙은 클래스를 전부 찾아 Bean으로 등록한다
-  직접 설정 또는 XML 설정
	@Bean 어노테이션을 등록하고 싶은 클래스 또는 메서드에 붙여 등록할 수 있다
	XML에서 설정하는법
	```XML
	<bean id="빈으로 등록되는 이름"
		class="빈으로 등록할 클래스 명">
		<property name="등록된 클래스가 의존 관계를 가지는 빈 이름", ref="참조명" />
	</bean>
```