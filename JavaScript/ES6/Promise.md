# Promise
## Promise란?
비동기 상태를 값으로 다룰 수 있는 객체다.  
Promise를 사용하면 비동기 프로그래밍을 할 때 동기 프로그래밍 방식으로 코드를 작성할 수 있다. 

## Promise 이해하기 
### 콜백패턴의 문제
자바스크립에서는 비동기 프로그래밍의 한 가지 방식으로 콜백 패턴을 많이 사용하였다. 하지만 콜백 패턴은 콜백이 조금만 중첩돼도 코드가 상당히 복잡해지는 단점이 있다.
```jsx 
function requestData1(callback){
 callback(data)
}

function requestData2(callback){
 callback(data)
}

function onSuccess1(data){
 requestData2(data)
}

function onSuccess2(data){
 console.log(data)
}

requestData1(onSuccess1);
```
콜백 패턴은 코드의 흐름이 순차적이지 않기 때문에 코드를 읽기가 상당히 힘들다. 짧은 코드임에도 쉽게 읽히지 않는다.
하지만 Promise를 사용하면 코드가 순차적으로 실행되게 작성이 가능하다 

### Promise 코드 예 
```jsx
requestData1()
 .then(data=>{
    return requestData2();
  })
  .then(data=>
    console.log(data)
  );
```

## Promise 세가지 상태 
Promise는 다음 세 가지 상태 중 하나의 상태로 존재한다 

- 대기중(pending) : 결과를 기다리는 중 
- 이행됨(fulfilled) : 수행이 정상적으로 끝났고 결괏값을 가지고 있음
- 거부됨(rejected): 수행이 비정상적으로 끝났음

이행됨, 거부됨 상태를 처리됨(settled)상태라고 부른다. 프로미스는 처리됨 상태가 되면 더 이상 다른 상태로 변경되지 않는다. 대기 중 상태일 때만 이행됨 또는 거부됨 상태로 변할 수 있다.

## Promise 생성방법
Promise는 다음 세가지 방식으로 생성 할 수 있다. 
```jsx
const p1 = new Promise((resolve,reject)=>{
  resolve(data);
  or reject('error message')
});

const p2 = Promise.reject('error message');
const p3 = Promise.resolve(param);
```

## Promise 이용하기 : then
then은 처리됨 상태가 된 프로미스를 처리할 때 사용되는 메서드이다. Promise가 처리됨 상태가 되면 then 메서드의 인수로 전달된 함수가 호출된다.
```jsx
requestData().then(onResolve,onReject);
Promise.resolve(123).then(data=>console.log(data)); // 123
Promise.reject('err').then(null,error=>console.log(error)); // 에러 발생
```
연속해서 then 사용하기 

```jsx
requestData1()
.then(data=>{
  console.log(data)
  return requestData2()
})
.then(data=>{
  return data + 1
})
.then(data => {
  throw new Error('some Error');
})
.then(data=>{
  console.log(error);
})
```

