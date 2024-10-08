서비스가 사용자를 대신해 다른 서비스에 접근해야하는 경우가 생기게 되는데, 이때 다른 서비스의 접근할 수 있는 정보인 ID와 Password를 서비스에 제공해야 한다 이렇게 되면, 서비스에 다른 서비스 정보를 넘기는 것이나 서비스에서 정보가 유출되면 다른 서비스의 정보도 유출되는 것이나 마찬가지이므로 보안적으로 이슈가 될 수도 있다.

이는 우리의 서비스와 구글, 페이스북, 트위터 등의 입장에서도 굉장한 부담이다. 우리의 입장에서는 사용자의 아주 민감한 정보를 직접 저장하고 관리해야한다는 부담이 생길 것 이다. 또한 구글, 페이스북, 트위터는 자신의 사용자 정보를 신뢰할 수 없는 제3자에게 맡긴다는 것이 매우 불만족스러울 것이다.

이를 해결하기 위해 구글과 야후는 독자적인 방법을 사용하여 해결하였지만 이는 표준화된 방식이 아니었기 때문에 해당 방식을 사용하기 위해서는 개별적으로 유지 보수 해야했다

그러다 OAuth 1.0이 등장하게 된다. 트위터와 Ma.gnolia 가 주도적으로 개발 이를 보완한 것이 OAuth 2.0이다.

다양한 플랫폼의 특정 사용자 정보에 접근하기 위해 제 3자 클라이언트가 사용자의 접근 권한을 위임받을 수 있는 표준 프로토콜이다.

### OAuth 2.0 주체
- Resource Owner
	서비스를 이용하면서 OAuth를 제공하는 플랫폼의 리소스를 소유하고 있는 사용자이다.
- Authorization & Resource Server
	Resource Owner를 인증하고 Client에게 액세스 토큰을 발급해주며, 리소스를 가지고 있는 서버이다.
- Client
	Resource Server의 자원을 이용하고자 하는 서비스이다.

![[OAuth 2.0.png]]
