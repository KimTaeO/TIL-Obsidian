 - 브라우저 작동원리
    * [[DNS]] 요청 시 DNS 서버가 해당 DNS주소에 대한 IP 주소 반환
	    이때 브라우저는 hosts 파일에서 DNS에 대한 호스트가 존재하는지 확인
	    DNS Cache에서 IP주소 확인
	    이때에도 존재하지 않는다면 DNS 서버에 질의
	    DNS Proxy로 작동하는 [[GSLB(Global Server Load Balancing)]]을 사용하기도 한다
    
    - 브라우저는 IP기반의 통신에서 [[3-Way-HandShake]] 기법으로 데이터를 주고받을 준비를 함
    
	* 클라는 HTTP 통신을 하여 서버로부터 response를 받아옴

	* 일련의 과정을 통해 [[Rendering Engine]]으로 화면을 그림

	- [[4-Way-HandShake]]를 수행하여 세션 종료