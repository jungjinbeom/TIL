# 호이스팅(Hoisting)

## 정의 
변수 및 함수 선언문이 스코프 내의 최상단으로 끌어올려지는 현상 
대입문은 끌어올려지지 않는다.
* 변수 선언문
```javascript   
console.log("호이스팅");
var test = "test";
let test2 = "test2";

//내부의 호이스팅 결과 
var test; //호이스팅 선언 
console.log("호이스팅")
test ="test"//할당
let test2 = "test2"//호이스팅 발생 x 
```
* 함수 선언문 
```javascript  
//함수 선언문도 호이스팅이 된다
 
func();
function func(){console.log("호이스팅")

//함수 표현식은 호이스팅 되지 않는다

func();
var func = function(){ console.log('변수 호이스팅') }
function func() {
  console.log('함수 호이스팅');
}
```
