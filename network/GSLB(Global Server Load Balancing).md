DNS 서비스의 발전된 형태로 
[[DNS]]는 하나의 호스트네임에 대하여 여러 IP주소를 제공할 수 있는데 이러한 기능을 사용하여 가용성과 로드밸런싱을 수행할수 있지만 근본적으로 한계가 있다.

그 이유는 DNS서버는 IP 목록 중 하나를 반환([[Round Robin]] 사용)할 뿐 서버의 상태를 고려한 로드 밸런싱을 하지 않기 때문이다. (네트워크 지연, 성능, 트래픽, 서비스 실패 등)

HealthCheck 기능 제공
	GSLB는 Host들에 대해 주기적으로 Health Check 요청을 보내 Unhealthy한 Host들은 로드밸런싱 대상에서 제외하여 요청 실패를 방지한다

* 재해복구
	실패한 서버는 응답에서 제외하므로 사용자는 서비스를 계속 이용할 수 있다
* 로드밸런싱
	트래픽이 몰리지 않은 서버의 IP를 반환하기 때문에 부하 분산이 가능하다
* 레이턴시 기반
	각 서버의 Latency를 가지고 있기 때문에 해당 유저로부터 Latency가 가장 낮은 서버의 IP를 반환한다
* 위치 기반
		유저의 지역 정보를 기반으로 가장 물리적으로 가까운 서버의 IP를 반환한다

GSLB는 DNS 프록시 기반으로 동작