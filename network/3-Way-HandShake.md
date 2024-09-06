SYN(synchronize sequence numbers), ACK(acknowledgment)
3-Way-HandShake란        
데이터를 전송하기 이전에 데이터를 정확하게 전송하기 위해 세션을 수립하는 과정    

1. 클라이언트(브라우저)는 서버에게 SYN플래그를 보냄 클라는 SYN_SENT 상태
2. 서버는 SYN플래그+ACK플래그를 클라이언트에게 반환 서버는 SYN_RECIEVED 상태
3. 클라이언트는 ACK플래그를 전송 이를 받으면 서로 ESTABLISHED 상태가 됨
4. 연결 성립


![[Pasted image 20240530170155.png]]
