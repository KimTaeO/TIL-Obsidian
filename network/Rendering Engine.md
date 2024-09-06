HTML과 CSS를 w3c명세를 따라 해석(Parsing)
    
- HTML을 Parsing하여 DOM Tree 생성

    - 렌더링 엔진이 style 태그 감지 시 Parsing을 중지 후 CSS Parsing을 시작
        CSSOM Tree 생성 시작
        
    - CSS Parsing이 끝나면 HTML Parsing 재개
        
    - 렌더링 엔진이 script 태그 감지 시 Parsing 중지 후 [[JS Engine]]에 제어 권한 위임
        JS Interpreter는 코드를 해석하여 AST(Abstract Syntax Tree)생성 후 실행
        
    - HTML Parsing이 완료되면 DOM Tree와 CSSOM Tree를 합쳐 Reder Tree 생성 (**이를 Construction 과정이라 함**)
        
    - Operation 과정
        
        - Render Tree의 Node들을 화면에 알맞게 표시하는 작업을 실행 (**이를 Layout 과정이라 함**)
            
        - UI Backend가 Render Tree의 Node들을 돌며 UI를 그림(**이를 Paint 과정이라 함**)
            
        - Node들의 Layer를 순서대로 구성하는 작업 실행(**이를 Composition 과정이라 함**)
            
            z-index가 낮은 것부터 순서대로 정렬
            
		빠르게 화면을 출력하기 위해 위의 일련의 과정을 서버로부터 모든 Response를 받고 나서 동작하는 것이 아닌 Response의 일부분을 받고 나서 화면을 출력하는 과정을 반복합니다.
