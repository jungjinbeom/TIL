# React-Query 
React-Query는 서버의 값을 클라이언트에 가져오거나 캐싱, 값 업데이트, 에러 핸들링 등 비동기 과정을 더욱 편하게 하는데 사용된다 

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
