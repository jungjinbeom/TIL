#ContextAPI 
##ContextAPI 란?
* 상위 컴포넌트에서 컴포넌트가 중간에 개입하지 않고 하위 컴포넌트로 직접 데이터를 전달 할 수 있는 API이다.

## Context API 사용 이유
- **ContextAPI 사용 전**
    * 기존에 상위 컴포넌트에서 하위 컴포넌트로 데이터를 내려줄 때 속성 값 (props)를 이용한다.
    * 상위 컴포넌트에서 하위 컴포넌트가 전달 해주려면 속성 값(props)을 내려주는 코드를 중첩적으로 작성해야하는 경우가 생긴다
    * 위와 같은 이러한 문제점을 해결하기 위해 **context API**를 사용한다.
    
##ContextAPI 사용법 
- **createContext**
    * **context** 객체를 만들때 사용하는 함수입니다.
    * **createContext**함수를 호출하면  **Provider**와 **Consumer** 컴포넌트를 반환합니다.
    * **defaultValue**는 초기값을 말합니다.(**Provider**를 사용하지 않았을 때 적용될 값)
- **Context.Provider**
   * **context**의 value를 변경하는 역할을 합니다.
   * **Provider**를 사용할 때에는 value를 꼭 명시해주어야만 동작함으로 주의합니다.
   * 전달받는 컴포넌트의 수는 제한이 없습니다.
- **Context.Consumer**
   * **context** 변화를 구독하는 컴포넌트를 말합니다.
   * 설정한 값을 불러와야 할 때 사용합니다. 
 ```jsx
   const UserContext = createContext();
    
    const UserComponent =()=>{
        return (
        <UserContext.Provider value='mike'>
            <UserContainer/>
        </UserContext.Provider>
        )
    }
    export default UserComponent;
    
    const UserContainer =()=>{
        return (
            <UserContext.Consumer>
                {username => <p> {`${username}`}</p>}
            </UserContext.Consumer>
        )
    }
    export default UserContainer;
```
* **Consumer** 에서는 값을 찾기 위해서 부모 컴포넌트, 즉 상위 컴포넌트로 올라가게 된다. 가장 가까운 **Provider**를 찾게되는데 만약 루트 컴포넌트까지 올라왔는데도 값 을 (value)를 찾지 못한다면 **createContext** 에서 정의한 값을 사용하게 된다. (ex. unknown)
* **Provider** 에 value값이 변경되면 하위의 모든 **Consumer** 컴포넌트는 다시 렌더링 된다
* **useContext**
    * **Consumer** 사용하지 않아도 데이터를 넘겨 받을 수 있고 jsx 영역이 복잡해지는 단점도 많이 개선이 된다
    * **Provider** 에서 받아온 값을 **Consumer** 컴포넌트 안쪽에서만 사용 할 수 있지만 **useContext** 는 전역으로 값을 사용할수 있다

## **Context 사용시 주의점**
* **<UserContext.Provider value={{username, age}}>** 이런 식으로 value안에다가 값을 입력하게되면 컴포넌트가 렌더링 될 때마다 객체가 다시 생성된다. 즉 내부 value값이 변경되지 않아도 **Consumer**는 매번 불필요하게 렌더링이 될 수 있다

    ```jsx
    const [username, setUsername] = useState('mike');
    const [age, setAge] = useState(23);
    ```

   매번 새로운 객체가 만들어지는 것을 방지 하기 위해  아래의 코드와 같이 하나의 객체로
   관리해주는게 좋다

    ```jsx
    const [user, setUser] = useState({username: 'mike', age: 23});
    <UserContext.Provider value={user}>
     </UserContext.Provider >
    ```

* **Consumer** 가 **Provider** 안에 감싸지도록 위치에 주의하여 사용해야한다.
    - **Consumer**가 **Provider**를 찾아 올라가는 과정에서 **Provider**를 찾지 못하면 결국에는 **createContext**에서 정의했던 초기 값을 사용하게 되는 경우가 생긴다. 이를 막기위해 사람들은 root에서 전체 jsx 코드를 감싸주게끔 **Provider**를 사용하는 경우도 많다.