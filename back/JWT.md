JSON Web Token의 약자로 JSON 포멧을 이용한 Claim기반의 웹 토큰이다
토큰 자체를 정보로 사용하는 Self-Contained 방식이다

JWT는 Header, Payload, Signature 세 부분으로 이루어져 있으며, 
Header에는 토큰 타입 암호화 방식이 들어가고

Payload는 사용자가 담고자 하는 Claim을 저장할 수 있으며
종류로는 Public/Private/Registered Claim이 있습니다

마지막으로 Signature에는 토큰을 인코딩하거나 유효성 검증을 할때 사용되는 부분이다.
Header와 Payload를 Base64로 인코딩 후
인코딩된 값을 secret Key로 헤더에서 정의한 알고리즘으로 해싱하고
이 값을 다시 Base64로 인코딩한 값이다