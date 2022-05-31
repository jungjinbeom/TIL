# 클로저
함수가 속한 렉시컬 스코프를 기억하여 함수가 렉시컬 스코프 밖에서 실행될 때도 그 스코프에 접근할 수 있게 하는 기능을 말한다.
```javascript
const outer = () => {
  const outerVariable = 'outer!'; // 1. outer 함수 안에 지역변수 outerVariable 선언

  const inner = () => {
    console.log(outerVariable); // 2. 바깥의 outerVariable을 참조해 console.log 출력
  };

  return inner; // 3. 바깥의 outerVariable을 참조해 console.log를 출력하는 함수를 반환
};

const fano = outer(); // 4. outer함수 호출 -> 변수 fano에 inner함수의 주소값이 저장됨

fano(); // 5. 'outer!'
//클로져는 어떤 함수(outer) 내부에 선언된 함수(inner)가 바깥 함수(outer)의 지역변수(outerVariable)를 참조하는 것이 함수(outer)가 종료된 이후에도 계속 유지되는 현상을 말합니다.
```
# 클로져가 발생하는 이유 
