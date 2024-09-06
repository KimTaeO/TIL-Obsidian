호스트 네임을 IP로 변환해 주는 디렉터리 서비스로 
계층 구조로 이루어진 분산 데이터베이스 형태이다

 Linux나 Unix 운영체제에서는 /etc/hosts 파일에 해당 도메인의 ip 주소 정보가 있는지 확인 
 local dns cache에 ip 주소 정보가 있는지 확인한다
 두 과정에서 해당 도메인에 대한 ip주소를 찾지 못하였다면 DNS 서버에 질의를 한다.

1. 사용자는 DNS 애플리케이션의 client측이 된다
2. 브라우저는 URL에서 추출한 hostname을 추출하고 DNS client에게 넘긴다
3. hostname을 포함한 질의를 DNS client는 DNS서버로 질의한다
4. DNS client는 hostname에 대한 IP 주소가 포함된 응답을 받게 된다
5. 브라우저가 DNS로부터 IP주소를 받으면 받은 IP주소를 통해 TCP 연결을 초기화한다

### DNS 서버를 찾는 법
[[DHCP]]를 이용하여 가장 가까운 DNS 서버의 IP 주소를 받아올 수 있다