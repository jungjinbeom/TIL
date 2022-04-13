# Spread operator(전개 연산자)
## 전개 연산자

- **배열이나 객체의 모든 속성을 풀어 놓을 때 사용하는 문법이다**
- **배열이나 객체를 복사할 때도 유용하다**

```javascript
//전개 연산자를 이용한 배열과 객체 복사 
const arr1 =[1,2,3]
const obj1 = {age:23,name:'mike'}

const arr2 = [...arr1]
console.log(arr2)

const obj2 = {...obj1}
console.log(obj2)

arr2.push(4)
console.log("after : ",arr2)
obj2.age=80
console.log("after : ",obj2)
// 전개 연산자를 사용해서 새로운 객체와 배열을 생성하였다 
// 새로운 객체가 생성되었기 때문에 속성을 추가하거나 변경해도 원래의 객체에 영향을 주지 않는다 
// 배열의 경우 전개 연산자를 사용하면 그순서가 유지된다 
//전개 연산자를 이용해서 두 객체를 병합하기 
const obj1 = {age:21,name:'mike'}
const obj2 = {hobby:'soccer'}
const obj3 = {...obj1 ,...obj2}
console.log(obj3)
const arr1 
```