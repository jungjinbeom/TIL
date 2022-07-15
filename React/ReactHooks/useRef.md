# **useRef**

## useRef란? 
어떠한 특정 DOM요소에 접근할 수 있게 해주는 React Hook이다
state가 변할때 마다 다시 렌더링 되면서 컴포넌트 내부 변수들이 초기화 되는데 원하지 않을때 렌더링을 방지하기 위해 Ref에 state값을 저장하면 state값이 변경되도 다시 렌더링 되지 않는다 이처럼 변수를 관리 할 때에도 사용된다.


### useRef 기본구조
```jsx
 const refContainer = useRef(initialValue);
```
### useRef 사용 예제
```jsx
import React, { useRef } from "react";

const App = () => {
  // 1. Ref객체 만들기
  const here = useRef();
  2. focus( ) DOM API 호출
  setTimeout(() => here.current.focus(), 3000);
  return (
    <div>
      <h1>Hello</h1>
      // 2. 원하는 곳에 ref 값으로 설정하기
      <input ref={here} placeholder="how are you" />
    </div>
  );
};
export default App;
```
1. useRef( )를 사용해 Ref객체 만들기
2. 해당 객체를 활용한 작업 설정 .current.focus()
3. 만든 Ref객체를 선택하고 싶은 DOM에 ref 값으로 설정하면 Ref객체의 .current값은 선택한 DOM을 가리키게 된다!

### useRef 변수 관리 예제 
1. useRef 특정 DOM을 선택하는 용도 이외에도 Component 안에서 조회 및 수정이 가능한 변수를 관리하는 용도로도 사용된다. 하지만 useRef 이용해서 변수를 업데이트 하게 되면 해당 Component가 리렌더링 되지 않기 때문에 리렌더링을 원한다면 callback ref를 사용해야 한다.

2. 관리되는 변수가 주로 쓰이는 곳
- setTimeout, setInterval을 통해 만들어진 id
- scroll의 위치
- 배열에 새 항목이 추가 될 때 필요한 고유 key 값
- 외부 라이브러리를 사용하여 생성된 인스턴스

```jsx
import React, {useRef} from 'react';
import UserList from './UserList';

//배열에 새 항목이 추가 될 때 필요한 고유 key 값 사용한 예제
const App = () => {
  const users = [
    {
      id:1,
      name: '김채원'
    },
    {
      id:2,
      name: '푸푸'
    },
    {
      id:3,
      name: '쌈무'
    }
  ];

  const nextId = useRef(4);
  const onCreate = () => {
    // 배열에 항목 추가하는 부분 생략
    nextId.current += 1; 
  };
  return <UserList users={users}/>;
}
export default App;
```

### useRef 사용 시 주의 점
```jsx
 <input type='text' ref={ref => ref && setText('initial text')}
        value={text} onChange={e => setText(e.taget.value)}/>
```
1. useRef 대신에 ref안에 속성값에 함수 입력도 가능하다. 함수는 해당하는 요소가 생성되거나 사라질 때 한번씩 호출되는데 생성될 때는 해당하는 값의 ref가 넘어오고 사라질 때는 null값이 넘어온다.
2. input 에 입력 할 때 마다 컴포넌트가 리렌더링 되면서 레퍼런스도 새로운 값이 만들어 지면서 값이 초기값이 고정되게 된다
3. 이를 해결하기 위해서 useCallback을 사용하게 된다.
```jsx
   const setInitialText=useCallback(ref => ref && setText('initial'), [])
    //useCallback의 메모이제이션 기능 덕분에 한번 생성해둔 함수를 계속해서 사용하게 된다
```

##참고 
[[TIL #13] React (Hooks) - useRef 란?](https://velog.io/@jminkyoung/TIL-13-React-Hooks-useRef-%EB%9E%80)
[[리액트] useRef, useEffect](https://velog.io/@suuhyeony/React-useRef-useEffect)
[useRef 로 컴포넌트 안의 변수 만들기](https://react.vlpt.us/basic/12-variable-with-useRef.html)
