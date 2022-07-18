# **useState**

## useState란?
* 함수형 컴포넌트에서 상탯값을 관리해주는 hook이다.
* 상태값 변경 함수는 비동기이면서 배치로 처리된다
* 상태값 변경 함수가 동기로 처리 되면 하나의 상태값 변경함수가 호출 될 때 마다 화면을 다시 그리기 때문에 성능 이슈가 생길 수 있다
* 이벤트 핸들러를 등록해서 사용하는 경우에도 리액트 내부에서 관리하지 않기 때문에 배치로 처리 되지 않는다
* 외부에서도 배치로 처리되기 원한다면 batchedupdate를 사용하여 배치로 처리한다
## 기본구조 
```jsx
const [counter,setCounter] = useState(initialState);
```
배열 비구조화 문법을 이용해 받는 것이기 때문에, counter,setCounter로 임의로 정할 수 있다.

## 사용 방법 
```jsx
import React,{useState} from 'react'
const Counter=()=>{
  const [counter,setCounter] = useState(0);
  return (
    <div>
      <span>{counter}</span>
    </div>
  )
}
```
## 하나의 useState()로 여러 상탯값 관리
```jsx
import React,{useState} from 'react'
const Profile=()=>{
  const [user,setUser] = useState({name:"",age:""});
  return (
    <div>
      <p>{`name is ${state.name}`}</p>
      <p>{`age is ${state.age}`}</p>
      <input type='text' value={state.name} 
             onChange={e=>setState({...state,name:e.target.value})}/>
      <input type='text' value={state.age} 
                onChange={e=>setState({...state,age:e.target.value})}/>
    </div>
  )
}
```

