# **useEffect**

## useEffect란?
- useEffect는 리액트 컴포넌트가 랜더링 될 때마다 특정 작업을 실행할 수 있도록 하는 Hook이다.
- useEffect는 component가 mount, unmount, update됐을때 특정 작업을 처리할 수 있다. 이는 클래스형 컴포넌트에서 사용할 수 있었던 생명주기 메소드를 함수형 컴포넌트에서도 사용할 수 있게  된것이다.


* 부수효과 처리
* 부수효과 : 외부의 상태를 변경하는것
* Ex) 서버 API 호출 , 이벤트 핸들러 추가
* useEffect Hook을 이용하여 우리는 리액트에게 컴포넌트가 렌더링 이후에 어떤 일을 수행해야하는 지를 말할 수 있다.
* 리액트는 우리가 넘긴 함수를 기억했다가(이 함수를 ‘effect’라고 부른다) DOM 업데이트를 수행한 이후에 불러낸다.
* Effect에서 함수를 반환하는 이유는 effect를 위한 추가적인 clean-up 메카니즘이다. 따라서 모든 effect는 정리를 위한 함수를 반환할 수 있다
* useEffectHook은 componentDidMount와 componentDidUpdate, componentWillUnmount가 합쳐진 것으로 볼 수 있다.
