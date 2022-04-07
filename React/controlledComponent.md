## 제어 컴포넌트
* 제어 컴포넌트는 컴포넌트의 상태나 속성(props)으로 주어진 값을 활용하는 컴포넌트다.
* input 태그를 제어 컴포넌트로 사용하느 예를 들어보면 value 값을 useState로 관리하는 것이 대표적인 예시이다

### 비제어 컴포넌트
* HTML 태그중에서 자체적으로 상태를 갖는 경우가 있다.
* 대표적인 경우가 값을 입력폼 내부의 상태(useRef)로 관리하며 DOM에서 폼 값을 가져올 수 있다.