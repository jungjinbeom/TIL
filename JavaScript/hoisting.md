# 호이스팅(Hoisting)

## 정의 
코드가 실행하기 전 **변수선언/함수선언**이 해당 스코프의 최상단으로 끌어 올려진 것 같은 현상을 말한다.

## 주의할 점 
호이스팅은 대입문을 끌어올려지고 대입문은 끌어 올려지지 않는다.
```jsx 
 //변수 선언문 
 var str;
 console.log(str) //undifined
 //변수 대입문 
 str="hello"
 console.log(str) //hello
```

## 변수 호이스팅
함수 호이스팅 과정에서 함수의 식별자를 선언하고 참조값을 초기화한 것처럼  
변수 또한 마찬가지로 선언과 초기화를 해주어야만 값의 참조 및 할당이 가능하다.  
다만 변수를 어떻게 선언 했는지에 따라, **선언, 초기화 시점이 달라질 수 있다는 점**을 유의해야한다.

# 변수 선언문
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

## 함수 호이스팅
함수 호이스팅이 가장 먼저 이루어진다. 함수의 선언문은 식별자가 변수 객체에 수집될 때  
부가적으로 함수의 참조에 대한 초기화 까지 자동으로 이루어지기 때문에 **상단에서 참조,호출이  
가능**하다.

# 함수 선언문 
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
