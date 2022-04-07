# 리액트 훅 (React hook)

## Hook이란?

* 컴포넌트에 기능을 추가할때 사용하는 기능
* **Hook**을 이용하여 기존 Class 바탕의 코드를 작성할 필요 없이 상태 값과 여러 React의 기능을 사용할 수 있습니다.

## Hook 사용 시 지켜야할 규칙

* 하나의 컴포넌트에서 훅을 호출하는 순서는 항상 같아야 한다.
    * 조건문, 반복문 함수 안에서 훅 사용 금지
* 훅은 함수형 컴포넌트 또는 커스텀 훅 안에서만 호출되어야 한다.
    * useState나 useEffect는 어떠한 id도 제공하지 않기 때문에 리액트 입장에서는 여러 개의 useState가 존재할 때 순서로 구분하기 때문에 순서가 중요하다
    
## Hook 종류
* **useState**
* **useEffect**
* **useContext**
* **useRef**
* **useMemo**
* **useCallback**
* **useReducer**
* **useDebugValue**
* **useImperativeHandle**
* **useLayoutEffect**
