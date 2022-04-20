#배열 및 객체 비구조화 할당

* 비구조화 할당은 객체와 배열로부터 프로퍼티를 쉽게 꺼낼 수 있는 문법입니다.
* 비구조화 할당 문법 역시 코드 줄 수를 상당히 줄여주므로 유용합니다. 특히 모듈을 주로 사용하는 노드의 경우 이러한 문법을 매우 자주 사용합니다

``` javascript
//객체의 프로퍼티를 같은 이름의 변수에 대입하는 코드이다 
let obj={
	name : "mike",
	age: "26",
};
const name = obj.name 
const age = obj.age

//비구조화 할당을 이용한 코드
let obj={
	name : "mike",
	age: "26",
};
const {name, age}=obj

 //객체를 나타내는 중괄호를 열고, 
 //그 안에 있는 프로퍼티들을 언급함으로써 간단하게 내용물을 꺼낼 수 있습니다.


//배열 안의 요소들을 비구조화 할당하는 코드 
const arr = ['string', {}, 1, true];
const [str, obj, , bool] = arr;

//ex)  console.log(str) => 'string'

//배열의 요소들은 순서대로 그 값들이 비구조화 할당이 됩니다. 
//따라서 str은 'string'가 obj에는 {}가 할당됩니다. 
//하지만 세 번째 요소는 비워둠으로써 할당하지 않았음을 알 수 있습니다

```