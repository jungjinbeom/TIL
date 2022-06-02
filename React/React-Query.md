# React-Query 
React-Query는 서버의 값을 클라이언트에 가져오거나 캐싱, 값 업데이트, 에러 핸들링 등 비동기 과정을 더욱 편하게 하는데 사용된다 

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
# 예시
```jsx
const Todos = () => {
  const { isLoading, isError, data, error } = useQuery("todos", fetchTodoList, {
    refetchOnWindowFocus: false, // react-query는 사용자가 사용하는 윈도우가 다른 곳을 갔다가 다시 화면으로 돌아오면 이 함수를 재실행합니다. 그 재실행 여부 옵션 입니다.
    retry: 0, // 실패시 재호출 몇번 할지
    onSuccess: data => {
      // 성공시 호출
      console.log(data);
    },
    onError: e => {
      // 실패시 호출 (401, 404 같은 error가 아니라 정말 api 호출이 실패한 경우만 호출됩니다.)
      // 강제로 에러 발생시키려면 api단에서 throw Error 날립니다. (참조: https://react-query.tanstack.com/guides/query-functions#usage-with-fetch-and-other-clients-that-do-not-throw-by-default)
      console.log(e.message);
    }
  });

  if (isLoading) {
    return <span>Loading...</span>;
  }

  if (isError) {
    return <span>Error: {error.message}</span>;
  }

  return (
    <ul>
      {data.map(todo => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
};
```

- useQuery : 데이터를 조회할 때 사용된다
 - useQuery는 키와 데이터를 불러오는 비동기 함수를 인자로 받아 어플리케이션의 현재 상태를 나타내는 다양한 값을 반환한다.
- useMutation : 서버 데이터를 등록, 업데이트, 삭제 할 때 사용된다.
 -  - useMutation 훅은 데이터를 업데이트 하기 위한 비동기 함수를 인자로 갖고 뮤테이션울 실행하기 위한 뮤테이트 함수를 반환한다 
