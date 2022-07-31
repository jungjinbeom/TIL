# Arrow Function(화살표 함수)
* ES6에는 화살표 함수를 이용해 함수를 정의하는 방법이 추가 되었다.
* ES5 에서는 function(){} 형태로 다루었는데, 화살표 함수를 사용하면 코드의 양을 줄이고 가독성이 개선 된다
* 자신을 감싸는 코드와 동일한 this 를 공유한다. 또한 표현식과 문에서도 사용할 수 있다.
```javascript
//add1, add2, add3은 모두 같은 로직을 수행하는 함수입니다
//사용하기에 따라서 중괄호를 생략이 가능하다  
//마지막 줄의 square 함수 같은 경우 파라미터 값이 하나일 경우 
//소괄호를 생략해서 값을 받을 수 있다 
const x = 1
const y = 2 
var add1 = function(x, y) {
  return x + y;
}
// 출력값 3

const add2 = (x, y) => {
  return x + y;
};
// 출력값 : 3

const add3 = (x, y) =>  x + y;
console.log(add3(1,2))
// 출력값 : 3

const square = x => x * 2;
// 출력값 : 4


// 표현식(expression)
var odds = evens.map(v => v + 1);
var nums = evens.map((v, i) => v + i);
var pairs = evens.map(v => ({even: v, odd: v + 1}));

// 문(Statement)
nums.forEach(v => {
    if (v % 5 === 0)
        fives.push(v);
});

// 렉시컬 this
var bob = {
    _name: "Bob",
    _friends: [],
    printFriends() {
        this._friends.forEach(f =>
            console.log(this._name + " knows " + f));
    }
}

```
