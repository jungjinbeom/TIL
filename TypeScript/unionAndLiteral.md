# Chapter3 유니언과 리터럴

## 유니언 (union)

타입을 두 가지 이상으로 확장하는 것

## 유니언 타입

- 타입의 값이 정확히 어떤 타입인지 모르지만 두개 이상 옵션 중 하나라는 것을 알고있는 경우 코드를 처리하는 개념을 **유니언**이라고 한다.
- **예제 코드**를 보면  **mathematician** 변수의 값은 **undefined** 혹은 **string**가 될 수 있는 것을 알수 있고 변수에 마우스를 가져가면 `let mathematician : string | undefined`로 타입이 간주되는 것을 알수 있다.

```tsx
let mathematician = Math.random()>0.5 ? undefined : "Mark Golberg";
```

## 유니언 타입 선언

- 유니언 타입을 타입 애너테이션으로 선언하여 사용이 가능하다.
- **예제 코드**를 보면 **thinker** 변수 초기값을 `null` 이지만 `null` 대신 `string` 값이 할당 될 수 있다는 것을 알 수 있다.

```tsx
let thinker : string : null = null;

if(Math.random() > 0.5){
	thinker = "Susanne Langer";
}
```

<aside>
💡 유니언 타입 선언의 순서는 중요하지 않다.

</aside>

## **유니언 속성**

- 타입 스크립트는 값이 유니언 타입일때 선언한 모든 타입에 존재하는 **값 속성에 접근이 가능**하다**.**
- 유니온 외의 타입에 접근하려고 하면 **타입검사 오류가 발생**한다.
- 예제코드에 `number | string`을  타입으로  선언하고 값의 속성을 사용할 때 `toUpperCase( )`는 에러가 발생한다.
- 이유는 `toString( )`는 number, string에 속성이 존재하고 `toUpperCase( )`는 string에만 존재하기 때문에 타입스크립트에서 존재 하지않는 속성에 대한 접근하여 에러 발생을 막으려는 안전장치이다.

```tsx
let physicist = Math.random()>0.5 ? "Marie Curie" : 84;

physicist.toString();

physicist.toUpperCase(); //error 
```

## 내로잉

- 값의 정의, 선언 혹은 이전에 유추된 것보다 더 **구체적인 타입**임을 코드에서 유추하는 것이다.
- 타입스크립트가 코드에서 타입을 좁혀 값을 구체적인 타입으로 취급하는데 이러한 타입을 좁히는데 사용되는 논리적 검사를 **타입가드**라고 한다.

## 흔히 사용되는 두가지 타입 가드

### 값 할당을 통한 내로잉

- 변수에 값을 할당하여 변수의 타입을 할당된 타입으로 좁히는 방식
- 예제코드에서 **admiral**에 문자열 값이 할당되었고 타입스크립트에서는  string으로 타입이 좁혀진 것을 알고 string 속성에 없는 `toFix()`속성 사용에 대해 타입 검사 오류를 발생 시킨 것을 알수있다.

```tsx
let admiral : number | string;

admiral = "Grace Hopper";// type string 

admiral.toUpperCase();

admiral.toFix(); //error

```

- 아래 예제코드에서 유니언 타입 선언하고 초기값을 문자열로 할당하면 타입스크립트는 문자열이 할당 되었기 때문에 타입이 string 타입으로 좁혀진 것을 알수있다.

```tsx
let admiral : number | string = "Grace Hopper";

admiral.toUpperCase();

admiral.toFix(); //error
```

### 조건 검사를 통한 내로잉

- 변수가 알려진 값과 같은지 확인하기 위해 **if**문을 통해 변수의 값을 좁히는 방법
- 예제코드에서 **if**문을 사용하여 변수의 값이 stirng 타입으로 좁혀진 것을 알수있다.

```tsx
// number | string 타입 
let scientist = Math.random() > 0.5 ? "Rosalind Franklin" : 51;

if(scientist === "Rosalind Franklin"){

// string 타입
 scientist.toUpperCase();
}

// number | string 타입 
scientist.toUpperCase(); //error
```

### typeof 검사를 통한 내로잉

- typeof 연산자를 사용하여 변수의 값을 좁히는 방법
- if문 조건으로 typeof 연산자를 사용하여 변수의 값 타입이 string인지 유추한 것을 알수있다.

```tsx
// number | string 타입 
let scientist = Math.random() > 0.5 ? "Rosalind Franklin" : 51;

if(typeof scientist === "string"){

// string 타입
 scientist.toUpperCase();
}
```

## 리터럴 타입

- 원시 타입 값 중 어떤 것이 아닌 **특정 원싯값**으로 알려진 타입이 리터럴 타입이다.
- 예제코드를 보면 타입이 string라고 알수 있는데 하지만 string 타입이 아닌 "Hypatia" 라는 특별한 타입이고 리터럴 타입의 개념이라고 알수있다.
- philosopher값에 마우스를 갔다대면 `const philosopher :"Hypatia"`  일반적인 원시타입 대신 리터럴 타입이 표시되는것을 알수있다.

```tsx
const philosopher = "Hypatia";
```

<aside>
💡 변수를 **const**로 선언하고 직접 리터럴 값을 할당하면 타입스트립트는 해당변수를 리터럴 값으로 유추한다.

</aside>

- 원시 타입은 해당 타입의 모든 리터럴 값의 집합이다.
- boolean, null, undefined 타입 외에 string, number과 같은 원시타입에는 무한할 수의 리터럴 타입의 있다.
    - **boolean** : true | false
    - **null과 undefined** : 자기자신 , 오직 하나의 리터럴 값만 가짐
    - **number** : 0 | 1 | 2…| 0.1 | 0.2….
    - **string** : “” | “a” | “b” |… | “aa” | “bb” |….
    
- 유니언 타입 애네테이셔에서는 리터널과 원시타입을 섞어서 사용이 가능하다.

```tsx
let lifespan: number | "ongoing" | "uncertain";

lifespan = 89;
lifespan = "ongoing";

lifespan = true; //error
```

- 리터럴 타입은 0,1 처럼 원시타입이 같아도 서로 다른 리터럴타입을 할당 할수 없다.

```tsx
let specificallAda :"Ada";

specificallAda = "Ada";

specificallAda = "Byron"; //error
```

### 엄격한 null 검사

- 타입 시스템에서 사용하는 **null**이나 **undefined** 값을 사용하지 못하게 하는 기능
- **십억 달러의 실수**를 잡기위해 도입한 타입스크립트의 기능
- 사용법은 `tsconfing.js`에서 `strictNullChecks : true` 설정해주면 된다 .
- `strictNullChecks`비활성화시 코드의 모든 타입에 null | undefined를 추가해야 모든 변수에 null 또는 undefined값을 할당 할수 있다.
- `strictNullChecks`활성화 시 코드가 null 또는undefined 값으로 인한 오류로 부터 안전한지 여부를 파악할 수 있다

### 십억달러의 실수

- 1965년 null 참조의 발명으로 수많은 오류, 취약성 및 시스템 충돌이 발생 했으며 지난 40년 동안 십억달러의 고통과 피해

### 참검사를 통한 내로잉

- 잠재적인 값중 truthy로 변수의 타입을 좁힐수 있다.
- &&연산자와 optional chaning은 참여부 확인 외 다른 기능을 제공하지 않는다.
- if~else를 사용하여 변수의 타입을 좁힐수 있다

```tsx
// string | undefined 타입 
//truthy를 사용한 참여부 확인
let gebeticist = Math.random() > 0.5 ? "Rosalind Franklin" : undefined;

if(gebeticist){
 gebeticist.toUpperCase();// string 타입
}

gebeticist.toUpperCase(); 
// Error : Object is possibly 'undefined'

// &&연산자와 optional chaning은 참여부 확인
gebeticist&& gebeticist.toUpperCase();
gebeticist?.toUpperCase()'

//if~else 참여부 확인
let biologist = Math.random() > 0.5 ? "Rosalind Franklin" : 0.5;
if(biologist){
	biologist// string 타입
}else{
	biologist // false | string 타입 
}
```

### 초기값 없는 변수

- 자바스크립트에서 초기값이 없는 변수는 기본적으로 undefined가 된다.
- 타입스크립트는 타입이 선언되어도 값이 할당 되기전까지 undefined로 인지한다.
- 값이 할당되기전에 접근시 예제코드와 같은 오류메시지를 나타낸다.

```tsx
let mathematician : string;

mathematician?.length;
//Error : Variavle "mathematician" is used before being assigned
```

- 변수 타입에 undefined를 추가하면 undefined는 유효한 타입이기 때문에 사용전에 값을 할당 하지 않아도 에러가 발생하지 않는다

```tsx
let mathematician : string | undefined;

mathematician?.length;
```

## 타입 별칭

- 반복성 유니언 타입 혹은 타입이 복잡해질 때 재사용 가능한 타입으로 할당하는 것
- type 새로운 이름 = 타입 형태를 가지며 타입 별칭은 파스칼 케이스로 이름을 짓는다.
- 타입 별칭은 타입스크립트에에만 존재하며 자바스크립트로 컴파일 되지 않는다.
- 타입 스크립트는 런타임에 존재하지 않아 런타임 코드에서 참조 할 수 없다
- 타입 별칭은 개발 시에만 존재한다.

```tsx
type RawData = boolean | number | string | null | undefined;

let rawDataFirst : RawData;
let rawDataSecond : RawData
let rawDataThrid : RawData

//런타임 코드
console.log(RawData);//error
```

## 타입 별칭 결합

- 기존에 만든 타입 별칭에 다른 타입 별칭을 참조하는 것

```tsx
type Id = number | string;

type IdMaybe Id | undefined | null;

//사용 순서대로 선언하지 않아도 된다 
type IdMaybe Id | undefined | null;
type Id = number | string;

```

<aside>
💡 사용 순서대로 타입 별칭을 선언 하지 않아도 사용이 가능하다

</aside>
