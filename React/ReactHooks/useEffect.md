# **useEffect**

## useEffect란?
- useEffect는 리액트 컴포넌트가 랜더링 될 때마다 특정 작업을 실행할 수 있도록 하는 Hook이다.
- useEffect는 component가 mount, unmount, update됐을때 특정 작업을 처리할 수 있다. 이는 클래스형 컴포넌트에서 사용할 수 있었던 생명주기 메소드를 함수형 컴포넌트에서도 사용할 수 있게  된것이다.
1. effect 함수 
- 렌더링 이후 실행할 함수 
- effect 함수에서 함수를 return 할 경우 그 함수가 컴포넌트가 Unmount 될 때 정리의 개념으로 한 번 실행된다.

2. deps
- 특정한 값이 변경될 때 effect 함수를 실행 하고 싶을 경우 배열안에 그 값을 넣어준다.
- 빈 배열일 경우 컴포넌트가 mount 될 때에만 실행된다.

<img src="../../images/생명주기.png">

* componentDidMount : 컴포넌트를 만들고 , 첫 렌더링을 다 마친 후 실행
* componentDidUpdate : 리렌더링을 완료한 후 실행, 즉 render()가 업데이트 될 때마다 실행
* componentWillUnMount : 컴포넌트를 DOM에서 제거할 때 실행

1. component가 Mount 되었을때 
```jsx 
  useEffect(()=>{
    console.log(렌더링 될 때 마다)
  })
```
```jsx 
  useEffect(()=>{
    console.log(맨 처음 렌더링 될 때 마다 )
  },[])
```
2. component가 update 되었을때 
```jsx 
  useEffect(()=>{
    console.log("name값이 업데이트 될때마다 실행")
  },[name])
```
특정값이 변경 될때마다 실행하고 싶을때는 deps에 특정값을 넣어준다 

3. Component가 Unmount 되었을때 
```jsx 
  useEffect(()=>{
    return ()=>{
      console.log("Unmount");
    }
  },[])
```
useEffect는 함수를 반환할 수 있는데 이 함수를 cleanup이라고 합니다.
Unmount 될 때만 cleanup 함수를 실행시키고 싶다면 deps에 빈 배열을
특정 값이 업데이트되기 직전에 cleanup 함수를 실행시키고 싶다면 deps에 해당 값을 넣어주면 됩니다.

# 참고 
[[React]리액트 Hooks : useEffect() 함수 사용법](https://cocoon1787.tistory.com/796)
[React - useEffect의 사용법과 예제](https://tocomo.tistory.com/32)
