# 변수(Variable)

## 변수란?
변수는 데이터를 담기 위한 공간을 의미한다.  
변수를 선언할 때는 var, let, const를 사용하여 선언 해야 한다.

## 자바스크립트 엔진의 변수 생성 3단계 
1. 선언 : 변수 이름을 등록해서 자바스크립트 엔진에 변수의 존재를 알린다.  
2. 초기화 : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undifined를 할당해 초기화한다.  
3. 할당 : undifined로 초기화된 변수에 실제값을 할당한다 

```jsx 
//변수 선언 및 초기화
let num;
//변수 할당
num = 10;

//변수 선언 및 할당 
let str ="hello";

//여러 변수 선언 및 초기화
let num, str;
//여러 변수 할당 
let num = 10, str= "hello";

//여러 변수  선언 및 힐당
let num = 10, str= "hello";
```

## 변수 끌어올림(호이스팅)

자바스크립트는 변수 선언이 어느 위치에 있든 맨 처음 선언을 미리 해둔다.  
이것을 호이스팅이라고 한다.  

호이스팅 전 
```jsx 
console.log(x)
var x;
```

호이스팅 후 
```jsx
var x;
console.log(x)
```


## 선언과 동시에 대입한 경우 
선언과 동시에 대입하는 코드는 끌어올리지 않는다.  
정확히는 선언부 var x는 끌어 올려지지만 , 대입부 x=5는 끌어 올려지지 않는다.  
```jsx 
console.log(x); // undifined
var x = 5;
console.log(x); // 5
```
호이스팅은 다른 언어에는 없는 자바스크립트만의 고유한 특징이나, 이해하기 쉬운 코드 작성을  
위해서는 **반드시 시작부에 변수를 선언**하는것이 좋다 

# 참고 자료 
[자바스크립트 변수(Variable)](https://velog.io/@yuuuye?tag=%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8)  
[JavaScript 변수란?](https://velog.io/@jungks9351/%EB%B3%80%EC%88%98)
