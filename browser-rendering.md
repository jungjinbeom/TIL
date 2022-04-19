#브라우저의 렌더링 원리 
브라우저가 화면에 나타나는 요소를 렌더링 할 때, 웹킷(Webkit)이나 게코 등과 같은 렌더링 엔진을 사용한다. 렌더링 엔진이 HTML, CSS, JavaScript로 렌더링할 때 CRP라는 프로세를 사용하며 다음단계들로 이루어진다.
1. HTML 파싱 후 DOM 트리 구축(Constructing the DOM Tree)
2. CSS 파싱 후 CSSOM 트리 구축(Constructing the CSSOM Tree)
3. JavaScript 실행(Running JavaScript)
4. DOM과 CSSOM 조합하여 렌더링 트리 구축(Creating the Render Tree)
5. 뷰포트 기반으로 렌터트리의 각노드가 가지는 정확한 위치와 크기 계산 후 레이아웃 생성(Generating the Layout)
6. 계산한 위치/크기를 기반으로 화면에 페인팅(Painting)
