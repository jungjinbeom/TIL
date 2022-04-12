#Template Literals(템플릿 리터럴)
* ES6에 추가된 템플릿 리터럴은 변수를 이용해서 동적으로 문자열을 생성할 수 있는 문법이다
* 템플릿 문자열은 기존 문자열과 다르게  백틱(`)을 사용합니다
* 백틱을 사용한 문자열은 문자열 안에 변수를 넣을 수 있습니다

##ES6 이전에 동적인 문자열을 생성하는 코드 
```javascript
var name = "mike";

var score ="80";
var msg = "name : "+name+", score/100 : " +score/100;
//출력값 
//name : mike, score/100 : 0.8
//매번 변수와 문자열을 '+' 로 이어줘야 한다 
```
##템플릿 리터럴를 사용한 코드
```javascript
const name = "mike";
const score ="80";
const msg = `name : ${name}, score/100: ${ score/100}`
//출력값 
//name : mike, score/100 : 0.8
//백틱 문자열 안에는 ${변수}형태로 삽입하기만 하면된다 
```