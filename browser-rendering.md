# 데이터를 받아오는 과정
1. www.naver.com을 입력하면 입력한 URL 주소 중 도메인 이름(naver.com)을 DNS 서버에서 검색한다. 
2. 가장 가까운 DNS 서버에서 해당 도메인 이름에 해당하는 IP주소를 찾아 사용자가 입력한 URL 정보와 함께 전달한다.
3. 전달받은 IP주소를 이용하여 웹 브라우저는 웹 서버에게 해당 웹사이트에 맞는 HTML문서를 요청한다.
4. 


# 브라우저의 렌더링 원리 
브라우저가 화면에 나타나는 요소를 렌더링 할 때, 웹킷(Webkit)이나 게코 등과 같은 렌더링 엔진을 사용한다. 렌더링 엔진이 HTML, CSS, JavaScript로 렌더링할 때 CRP라는 프로세를 사용하며 다음단계들로 이루어진다.
1. HTML 파싱 후 DOM 트리 구축(Constructing the DOM Tree)
2. CSS 파싱 후 CSSOM 트리 구축(Constructing the CSSOM Tree)
3. JavaScript 실행(Running JavaScript)
4. DOM과 CSSOM 조합하여 렌더링 트리 구축(Creating the Render Tree)
5. Rendering Tree에서 각노드가 가지는 정확한 위치와 크기 계산 후 레이아웃 생성(Generating the Layout)
6. 계산한 위치/크기를 기반으로 화면에 페인팅(Painting)
7. 레이어를 합성하여 실제 화면에 나타낸다(Composite)
<img src="./images/브라우저 렌더링.png">
