# React-Query 
 
## React-Query란? 
React-Query는 데이터 Fetching, 캐싱, 동기화 서버쪽 데이터 업데이트 등을 쉽게 만들어 주는 React 라이브러리


## React-Query 훅 
useQuery
- 서버로 부터 데이터를 조회해올때 사용되는 hook이다

### useQuery 작성 및 구현을 위한 2가지 개념 
- queryKey   
  - use Query마다 부여되는 고유 Key 값 이다. 
  - 해당 key 값은 단순하게 문자열로 사용될 수도 있고 배열의 형태로도 사용이 가능하다.
  - React Query가 query 캐싱을 관리할 수 있도록 도와준다 
   ```jsx
    //문자열 
    const res = useQuery('person',queryFn);

    //배열 
    const res = useQuery(['person','add Id'],queryFn);
   ```
- queryFn
  - queryFn은 query Function으로 promise처리가 이루어지는 함수이다.
  - 쉽게 말하면 axios를 이용해 서버에 API 요철하는 코드라고 생각하면된다. 
  ```jsx
    const res = useQuery({queryKey : ['person'],queryFn: ()=> axios.get('http://localhost:8080/persons')});
   ```
 
 ### useQuery 사용 방법 
 ```jsx
import { QueryClient, QueryClientProvider, useQuery } from '@tanstack/react-query'

const queryClient = new QueryClient()

function Example() {
  const query = useQuery('todos', fetchTodos)

  return (
    <div>
      {query.isLoading
        ? 'Loading...'
        : query.isError
        ? 'Error!'
        : query.data
        ? query.data.map((todo) => <div key={todo.id}>{todo.title}</div>)
        : null}
    </div>
  )
}
 ```
 
useQueries

useMutation
  데이터 조회가 아닌 데이터 변경 작업을 할때 사용되는 hook이다 
# React-Query 라이프 사이클 
* fetching-데이터 요청 상태
* fresh- 데이터가 프레시한(만료되지 않은) 상태.
  * 컴포넌트의 상태가 변경되더라도 데이터를 다시 요청하지 않는다.
  * 새로고침 하면 다시 fetching 한다.
* stale - 데이터가 만료된 상태.
* 데이터가 만료되었다는 것은 서버에서 한번 프론트로 데이터를 주면 그 사이에 다른 유저가 데이터를 추가, 수정, 삭제 등등 할 수 있기 때문에 만료되었다고 한다. (최신화가 필요한 데이터)
* 컴포넌트가 마운트, 업데이트되면 데이터를 다시 요청합니다.
* fresh에서 stale로 넘어가는 시간 -> 기본값 0
* inactive - 사용하지 않는 상태.
  * 일정 시간이 지나면 가비지 콜렉터가 캐시에서 제거함
  * 기본값 5분
* delete - 가비지 콜렉터에 의해 캐시에서 제거된 상태.

# 장점
 - 서버 데이터 캐싱 
 - 데이터 패칭 시 로딩, 에러 처리를 한 곳에서 처리 가능 
 - 비동기 과정을 선언적으로 관리 할 수 있다. 
 - react hook와 사용하는 구조가 비슷하다.
 - 쉬운 상태 관리 
 - 중복 요청 제거 
 - 편리한 디버깅 툴 
 - SSR, Next,js 지원 
