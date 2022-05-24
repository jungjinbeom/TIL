# let, const
## 변수를 정의하는 새로운 방법
* ES5 까지는 자바스크립트에서 var를 사용해서 변수를 정의해왔다. 하지만 ES6 문법 부터는 더 이상 var를 사용하지 않고 const 와 let 을 사용한다.
* const,let : 블록 스코프 , var : 함수 스코프
 ```javascript
if (true) {
var x = 'var로 선언한 변수입니다.';
}
console.log(x);
//(출력값) var로 선언한 변수입니다. 
//함수 스코프여서 스코프에 접근이 가능하다*

if (true) {
const y = 'const로 선언한 변수입니다.';
}
console.log(y);
// (출력값) ReferenceError: y is not defined
// 블록스코프여서 스코프에 선언한 변수에 접근을 못한다 
```

## const,let의 차이점 
* const 는 정의된 변수는 재할당이 불가능하다
* let은 재할당이 가능하다
```javascript
const bar = "a";
bar ="b" //에러발생
var foo = "a";
foo="b"// 에러 없음
let value="a";
value ="b"//에러없음
```
* 재할당 불가능한 변수는 프로그램의 복잡도를 상당히 낮춰주기 때문에 되도록이면 재할당 불가능한 변수를 사용하는 것이 좋다
* 변수선언 시에는 const  선언하고 다른 값을 대입 해야 할 상황이 생겼을 때는 let을 사용하는 것이 좋다
