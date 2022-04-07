# **useRef**

* 렌더링과 무관한 값을 저장할 때 사용된다
* 현재의 값과 이전의 값을 비교할 때 사용
* .current 프로퍼티에 변경 가능한 값을 담고 있는 '상자'와 같다.
* ref는 실제 돔 요소에 직접 접근 하고 싶은 경우가 생길 때 사용가능하다.
* Current : 여기서 current는 실제 돔 요소를 가리키게 된다. 따라서 실제 돔에 있는 focus함수가 실행할 수 있게 된다. 실제 돔 요소는 렌더링 결과가 실제 돔에 반영된 후에 접근 가능하기 때문에 부수 효과 함수 (useEffect) 안에서 접근 가능하게 된다.
* useRef 사용 시 주의 점

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