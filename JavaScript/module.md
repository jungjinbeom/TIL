# 모듈 시스템

## 모듈이란?
여러 기능들에 관한 코드가 모여있는 하나의 파일
유지보수성, 네임스페이스화, 재사용성 의 특징을 가지고 있다 

## Common JS
자바스크립트의 공식 스펙의 브라우저만 지원했다 하지만 서버사이드 및 데스크탑 애플리케이션에서 지원하기 위한 노력 중이다.
```jsx
/ 내보내기
export { something }
// 가져오기
import { something } from './파일명'
// 모든 객체를 가져오되 원하는 이름을 붙여서 사용가능
import * as obj from './파일명'

// default 키워드
export default 내보낼 변수명
// default 키워드를 이용한 경우, 내보낸 쪽에서 사용한 명칭을 그대로 사용하지 않아도 된다.
import 바꿀변수명 from './파일명'
```
## AMD
CommonJS 그룹에서 의견이 맞지 않아 나온 사람들이 만든 그룹으로 비동기 모듈에 대한 표준안을 다루는 그룹이다. 
CommonJS가 서버쪽에서 장점이 많은 반면에 AMD는 브라우저 쪽에서 더 큰 효과를 발휘한다. 
이를 구현한 가장 유명한 스크립트가 RequireJS 이다.
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Document</title>
</head>
<body>
  <script data-main="index.js" src="require.js"></script>
</body>
</html>
```
require.js 파일을 받아서 <script> 태그에 넣어주고 data-main 속성으로 require.js 가 로드된 후에 실행할 자바스크립트 파일 경로를 넣어준다. 즉, require.js 가 로드되자마자 index.js 가 실행되는 구조이다.
  
 * a.js
  
```javascript
define(() => {
  return {
    printA: () => console.log('a')
  }
});
```
모듈 a는 위와 같이 만들어져 있고 define() 을 통해서 정의된다. 여기서도 require() 에서 의존성 모듈을 설정해준 것처럼 콜백함수가 실행되기 전에 로드되어야 할 모듈들을 지정해줄 수 있다.

