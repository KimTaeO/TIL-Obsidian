Spring에서 [[Bean]]의 생성과 관계 설정과 같은 제어를 담당하는 IoC 컨테이너인 Bean Factory가 존재한다. 하지만 실제로는 추가적인 기능이 필요한데 이를 위해 Bean Factory를 상속받아 확장한 Application Context라는 것이 있다

Application Context는 별도의 설정 정보를 참고하고 IoC를 적용하여 Bean의 생성, 관계 설정 등의 제어 작업을 총괄한다.

Application Context에서는 Bean을 직접 생성하지 않고 관계를 맺지 않고, 생성 정보와 연관관계 정보에 대한 설정을 읽어 처리한다 
@Configuration과 같은 어노테이션이 대표적인 IoC 설정 정보이다.

Application Context는 @Configuration이 붙은 클래스들을 설정 정보로 등록해두고 @Bean이 붙은 메서드의 이름으로 Bean 목록을 생성한다
클라이언트가 Bean을 요청하면 Application Context는 Bean 목록에서 요청한 이름이 있는지 찾는다. 있다면 설정 클래스로부터 빈 생성을 요청하고 생성된 빈을 돌려준다.

클라이언트는 @Configuration붙은 설정 정보 클래스를 알 필요가 없다

Application Context는 종합 IoC 서비스를 제공해준다

Application Context를 통해 다양한 빈 검색 방법을 제공할 수 있다