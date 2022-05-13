# Recoil
API와 의미 및 동작을 가능한 React답게 유지하면서 React의 상태관리와 관련된 한계점을 개선하고자 페이스북에서 React를 위해 만든 상태관리 라이브러리이다. Recoil은 React처럼 작동하며 파생데이터와 비동기 쿼리는 순수 함수와 효율적인 구독으로 관리된다.

# Recoil 주요 개념 
* **Atoms**
  * Atoms는 상태의 단위이며, 업데이트와 구독이 가능하다.
  * atom이 업데이트 되면 각각의 구독된 컴포넌트는 새로운 값을 반영하여 다시 렌더링된다.
  * 동일한 atom이 여러 컴포넌트에서 사용되는 경우 모든 컴포넌트는 상태를 공유할 수 있다 
  
  ``` jsx
  const fontSizeState = atom({
    key: 'fontSizeState',
    default: 14,
  });
  ```
  * Atoms는 디버깅 , 지속성 및 모든 atoms의 map을 볼 수 있는 **고유한 키(unique key)**가 필요하며 고유한 키이기 때문에 두개의 atom이 같은 키를 가질 수 없으며 키 값은 전역적으로 고유해야한다.
  * 컴포넌트에서 atom을 읽고 쓰려면 **useRecoilState** 라는 훅을 사용해야한다. useState와 비슷하지만 상태가 컴포넌트 간에 공유 될 수 있다는게 차이점이다.
  
  ```jsx
    function FontButton() {
    const [fontSize, setFontSize] = useRecoilState(fontSizeState);
    return (
      <button onClick={() => setFontSize((size) => size + 1)} style={{fontSize}}>
        Click to Enlarge
      </button>
    );
  }
  ```
* Selectors
  * Selector는 atoms나 다른 selectors를 받아 데이터를 가공하여 리턴하는 순수 함수이다.
  * 상위의 atoms나 또는 selectors가 업데이트 되면 하위 selector 함수도 다시 실행한다.
  * 모든 컴포넌트들은 selector를 atoms처럼 구독할 수 있고 selectors가 변경되면 구독중인 컴포넌트들도 리렌더링 된다.
  * 최소한의 상태 집합만 atoms에 저장하고 다른 모든 파생되는 데이터는 selectors에 명시한 함수를 통해 효율적으로 계산함으로써 쓸모없는 상태의 보존을 방지한다.
  * selectors는 자신을 구독한 컴포넌트 그리고 의존하는 상태의 값을 추적한다.
  ```jsx
   const fontSizeLabelState = selector({
    key: 'fontSizeLabelState',
    get: ({get}) => {
    const fontSize = get(fontSizeState);
    const unit = 'px';

    return `${fontSize}${unit}`;
  })
  ```
  * get 속성은 계산될 함수이다. 전달되는 get인자를 통해 atoms와 다른 selectors에 접근 할 수 있다. 다른 atoms나 selectors에 접근하면 자동으로 종속 관계가 생성되므로, 참조 했던 다른 atoms나 selectors가 업데이트되면 이 함수도 다시 실행된다 
  * Selectors는 **useRecoilValue()**를 사용해 읽을 수 있다. **useRecoilValue()**는 하나의 atom이나 selector를 인자로 받아 대응하는 값을 반환한다.
  ```jsx
    const fontSizeLabel = useRecoilValue(fontSizeLabelState);
  ```
  # RecoilHooks
  * useRecoilState
   * atom의 상태를 설정하고 변경 시킬 수 있다.
  * useRecoilValue
   * atom의 상태값을 조회 할 때 사용한다.
  * useSetRecoilState
   * setter 역할을 하며 useSetRecoilState 사용하여 atom의 값을 변경 할 수 있다.
  * useResetRecoilState
   * atom의 값을 default값으로 변경 시킨다.
