# 실행 컨텍스트 Execution Context
## 정의
* scope, hoisting, this, function, closure 등의 동작원리를 담고 있는 자바스크립트의 핵심 원리
* 코드의 실행환경에 대한 여러가지 정보를 담고있는 개념
* 자바 스크립트 엔진에 의해 만들어지고 사용되는 코드 정보를 담은 객체의 집합이라고 할 수 있다.
* 실행 컨텍스트는 실행 가능한 코드가 실행되기 위해 필요한 환경

## 종류 
* 자바스크립트의 코드는 3가지 종류로 이루어지고 자신만의 실행 컨텍스트를 생성한다
    * 전역 코드 : 전역 영역에 존재하는 코드
    * Eval 코드 : eval 함수로 실행되는 코드
    * 함수 코드 : 함수 내에 존재하는 코드 
* 엔진이 스크립트 파일을 실행하기 전에 글로벌 실행 컨텍스트(Global Execution Context, GEC) 가 생성되고, 함수를 호출할 때마다 함수 실행 컨텍스트(Function Execution Context, FEC) 가 생성된다. 주의할 점은, 글로벌의 경우 실행 이전에 생성되지만 함수의 경우 호출할 때 생성된다는 점이다.
## 실행 컨텍스트 스택(Execution Context Stack)
* 실행 컨텍스트가 생성되면 흔히 콜 스텍이라고 불리는 실행 컨텍스트 스택에 쌓이게 된다 스택은 LIFO(Last In First Out, 후입 선출)의 구조를 가지는 나열 구조이며
GEC는 코드를 실행하기 전에 쌓이고 모든 코드를 실행하면 제거된다. FEC는 호출 할 때 쌓이고 호출이 끝나면 제거된다.
  
## 실행 컨텍스트의 상태 구성 
* Lexical Environment
* Variable Environment
* This Binding 
## Lexical Environment
 Lexical Environment는 변수 및 함수 등의 식별자 및 외부 참에 관한 정보를 가지고 있는 컴포넌트이며 2가지의 구성요소를 가지고 있다 
* Environment Record가 식별자에 관한 정보를 가지고 있으며 outer 참조는 외부 Lexical Environment를 참조하는 포인터이다.
```javascript 
  var x = 10;

  function foo() {
  var y = 20;
  console.log(x);
  }
```
위와 같은 코드가 있을 때는 아래와 같이 Lexical Environment가 형성된다.
```
  globalEnvironment = {
    environmentRecord = { x: 10 },
    outer: null
  }
  fooEnvironment = {
    environmentRecord = { y: 20 },
    outer: globalEnvironment
  }
```
따라서, foo() 에서 x 를 참조할 때는 현대 Environment Record를 찾아보고 없기 때문에 outer 참조를 사용하여 외부의 Lexical Environment에 속해 있는 Environment Record를 찾아보는 방식이다.

## Variable Environment
Lexical Environment 에 포함되는 개념으로 Variable Object 에는 변수, 함수선언, 함수 매개 변수 들을 저장한다. 이는 코드에 의해 새로운 변수/함수가 추가되더라도 절대 값이 변하지 않는다.
## this 바인딩
this의 바인딩은 실행 컨텍스트가 생성될 때마다 this 객체에 어떻게 바인딩이 되는지를 나타낸 것이다. (ES6부터 this의 바인딩이 LexicalEnvironment 안에 있는 EnvironmentRecord 안에서 일어난다

