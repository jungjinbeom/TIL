# 5.1 함수 매개변수

song을 매개변수로 받아 콘솔 로그로 찍는 함수이다.

```tsx
function sing(song){
	console.log(`Singing : ${song}!`);
}
```

위 함수처럼 매개변수에 타입이 선언되어있지 않으면 타입스크립트는 이를 **any타입으로 간주**하고 매개변수의 타입은 무엇이든 될 수 있다.

- 매개변수에 타입이 선언되지 않아 어떠한 타입의 값이 들어올 수 있다.
- 타입이 불분명해 오류나 버그를 유발 할 수 있다.
    - 예시
    - 타입 맞지 않는 메서드를 사용하여 에러가 발생 할 수 있다.

아래의 코드는 타입 애너테이션으로  함수의 매개변수의 타입을 선언한 코드이다. 

```tsx
function sing(song:string){
	console.log(`Singing : ${song}!`);
}
```

매개변수에 타입 선언되어 무슨 타입인지 확실해졌다 

- 이렇게 함수의 매개변수에 타입을 추가해서 타입 안정성을 강화한 함수를 **선언전 함수**라고 한다.
- 타입오류의 오류를 미리 알고 사전에 방지 할 수 있다.

# 5.1.1 필수 매개변수

- 자바스크립트에서는 인수의 수와 상관없이 함수 호출이 가능하다.
- 타입스크립트는 함수에 선언된 **모든 매개변수가 필수**라고 가정한다.
함수를 호출 할 때 **지정한 파라미터의 갯수**와 호출 할때 넘겨주는 **인자의 갯수가** 타입스크립트는 **오류의 형태로 이의를 제기**한다.

아래 코드로 예시를 들어 보겠습니다.

```tsx
function singTwo(first: string, second: string){
	console.log(`${first} / ${second}`)
}

singTwo("Ball and Chain");
//Error : Expected 2 arguments, but got 1

singTwo("I Will Survive", "Higher Love");
//Ok

singTwo("Chain", "and", "Ball");
//Error : Expected 2 arguments, but got 3
```

위와 같이 함수에 호출 시 **지정한 파라미터의 갯수**와 호출 할때 넘겨주는 **인자의 갯수**가 같지 않으면 에러를 발생시킨다

- 함수에서 필수 매개변수를 제공 하도록 강제하면 예상되는 인수의 갯수를 유추 할 수 있으며 타입 안정성에도 도움이 됩니다.
- 함수의 매개변수를 설정하면 **undefined나 null이라도 인자로 넘겨야**하며 컴파일러에서 정의된 매개변수 값이 넘어 왔는지 확인한다.
- 매개변수는 인수로 받을 것으로 예상되는 함수의 선언을 나타냅니다. 인수는 함수를 호출 할 때 매개 변수에 제공되는 값을 나타낸다.

<aside>
💡 **인수(arguments)란**?

함수가 호출할 때 함수로값을 전달해주는 값을 말한다.

(1) 함수의 매개변수보다 적게 인수를 전달할 경우와 전달되지 않은 인자에는 undefined 값이 할당된다.
(2) 매개변수보다 많게 인수를 전달 할 경우 초과된 인수는 무시되지만 arguments라는 객체에 할당된다.

(3) arguments는 지역변수이며, arguments 객체를 통하여 초과로 전달된 인수를 참조할 수 있다.

</aside>

# 5.1.2 선택적 매개변수

- 자바스크립트에서는 함수의 내부 인숫 값이 기본적으로 undefined가 기본 값으로 설정된다.
- 타입스크립트에서는 매개변수에 선언한 **타입 애너테이션에 “ : “ 앞에 ?를 추가해 매개변수를 선택적으로 받을 수 있다.**
- 선택적 매개변수에는 항상 | undefined가 유니언타입으로 추가 되어 있다.

```tsx
function announceSong(song: string , singer ?: string){
	console.log(`Song : ${song}`);

	if(singer){
		console.log(`Singer: ${singer}`);
	}
}

announceSong("Greensleeves"); //ok
announceSong("Greensleeves",undefined); //ok
announceSong("Greensleeves","Sia"); //ok
```

- 선택적 매개변수에 | undefined를 사용하면 **매개변수값에 undefined값을 항상 넘겨줘야한다**.

```tsx
function announceSong(song: string , singer ?: string | undefined){
	console.log(`Song : ${song}`);

	if(singer){
		console.log(`Singer: ${singer}`);
	}
}

announceSong("Greensleeves"); //error
//Error  : Expected 2 arguments, but got 1.

announceSong("Greensleeves",undefined); //ok
announceSong("Greensleeves","Sia"); //ok
```

- 함수에서 사용하는 선택적 매개변수의 위치는 **마지막**이여야 한다.
- 위치가 마지막이 아닐 경우 타입스크립트에서 구문오류가 발생한다.

```tsx
function announceSinger(singer?:string, song : string){}

//error : A required parameter cannot follow an optional parameter
```

# 5.1.3 기본 매개변수

- 위에 글에서 설명한 것 처럼 선택적 매개변수를 사용하면 암묵적으로 | undefined 유니언타입이 추가된다.
- 타입스크립트는 **매개변수에 기본 값이 있고 타입 애너테이션이 없는 경우** 해당 기본값을 기반으로 **매개변수 타입을 추론**한다.
- **매개변수에 기본 값이 있고 타입 애너테이션이 없는 경우**선택적 매개변수로 작동한다.

```tsx
function rateSong(song:string, rating = 0){
	console.log(`${song} gets ${rating}/5 stars!`)
}

rateSong("PhotoGraph");//ok
rateSong("PhotoGraph", 5); //ok
rateSong("PhotoGraph", undefined); //ok

rateSong("PhotoGraph", "100"); //error
//Error " Argument of type "100" is not assignable to 
// parameter of type 'number | undefined'.

```

# 5.1.4 나머지 매개변수

- **나머지 매개변수**는 (마지막 매개변수 위치에 스프레드 연산자로 선언) 함수에서 **여러인자를 배열로 받는다**.
- 타입스크립트는 이러한 **나머지 매개변수**의 타입을 일반 매개변수와 유사하게 선언할수 있다. 하지만 인수 배열을 나타내기 위해 **끝에 [] 구문을 추가**해야된다.

```tsx
function singAllTheSongs(singer : string, ...songs : string[]){
	for(const song of songs){
		console.log(`${song}, by ${singer}`);
	}
}

singAllTheSongs("Alicia Keys");//ok
singAllTheSongs("Lady Gaga","Bad Romance","just Dance","Poker Face"); //ok

singAllTheSongs("Ella Fitzgerald", 100); //error
//Error " Argument of type 'number' is not assignable to 
// parameter of type 'string'.

```

 

# 5.2 반환 타입

- 타입 스크립트는 지각적(알아서 깨닫는)이다
- 함수가 반환 할수 있는 가능한 모든 값을 이해하면 함수가 반환하는 타입을 알 수 있다.
- 아래의 코드 예제에서 singSong는 타입스크립트에서 number를 반환하는 것을 유추 할 수 있다.

```tsx
function singSongs(songs : string[]){
	for(const song of songs){
		console.log(`${song}`);
	}
	return songs.length;
}
```

- 함수는 **다른 값을 가지 여러 개의 반환문**을 포함하고 있다면, 타입스크립트는 **반환 타입을 가능한 모든 반환 타입의 조합으로 유추** 할 수 있다

```tsx
//타입 : (songs : string[], index: number) =>string | undefined
function getSongAt(songs : string[], index : number){
	return index < songs.length 
			? songs[index] 
			: undefined;
}
```

# 5.2.1 명시적 반환 타입

- 함수의 **반환 타입을 명시적으로 선언하지 않는 것이 좋다** 하지만 **반환타입을 명시적으로 선언하는 방식이 유용 할때가 있다.**
    - 가능한 반환값이 많은 함수가 항상 동일한 타입의 값을 반환하도록 강제 할 수있다.
    - 타입 스크립트는 재귀 함수의 반환 타입을 통해 타입을 유추하는 것을 거부한다.
    - 수백 개 이상의 타입스크립트 파일이 있는 매우 큰 프로젝트에서 타입스크립트 타입 검사 속도를 높일 수 있다.
    
    반환 타입의 선언 위치 
    
    ```tsx
    //함수 선언시
    function singSongsRecursive(songs:string[], count=0):number {}
    
    //함수 표현식
    const singSongsRecursive = (songs:string[], count=0):number => {}
    ```
    
    반환 타입이 명시적으로 선언되었을 경우
    
    - 반환 타입에 맞지않는 타입을 return 할 경우 타입스크립트에서 에러를 나타낸다.
    
    ```tsx
    //
    function singSongsRecursive(songs:string[], count=0):number | undefined {
    	return count ? 1 | "100"
    	//Error : Type 'string' is not assignable to type "Date"
    }
    ```
    
    # 5.3 함수 타입
    
    - 자바스크립트는 함수를 값으로 전달 할 수 있다.
    - 타입스크립트에서 함수를 매개변수로 넘겨 받거나 변수에 할당 할때 타입을 선언 해줘야한다.
    - 아래의 코드는 변수타입은 매개변수가 없고 string 타입을 반환하는 함수이다.
    
    ```tsx
    let nothingInFivesString : () => string;
    ```
    
    - 아래의 코드는 string[] 매개변수와 count  선택적 매개변수 및 number 값을 반환하는 함수이다.
    
    ```tsx
    let inputAndOutput : (songs:string[],count?:number) => number;
    ```
    
    - 함수 타입은 콜백 매개변수(함수로 호출되는 매개변수)를 설명하는데 자주 사용된다
    - runOnSongs 함수는 getSongAt 매개변수의 타입을 index: number를 받고 string 을 반환하는 함수로 선언했다
    - getSongAt 함수를 매개변수로 넘겨주면 해당 타입이 일치해서 작동한다.
    - logSong 매개변수로 number 대신 string을 사용하여 반환값을 받아오는데 실패하고 타입스크립트는 에러를 발생시킨다.
    
    ```tsx
    const songs =["Juice", "Shake it Off", "What`s Up"];
    
    function runOnSongs (getSongAt: (index: number) => string){
    	for(let i = 0; i < songs.length; i+=1){
    		console.log(getSongAt(i));
    	}
    }
    function getSongAt(index:number){
    	return `${songs[index]}`;
    }
    
    runOnSongs(getSongAt)// ok
    
    function logSong(song:string){
    	return `${song}`;
    }
    
    runOnSongs(logSong);//error
    //
    
    //Error: Argument of type '(song: string)=> string' is not 
    //Assignable to parameter of type '(index:number)=> string'
    
    // Type of parameters 'song' and 'index' are incompatible.
    
    // Type "number" is not assignable to type 'string'.
    ```
    
    - runOnSongs(logSong)에 대한 오류 메시지는 할당 가능성 오류의 예로 몇 가지 상세한 단계까지 제공한다.
    
    > **1.** 첫번째 들여쓰기 단계는 두 함수 타입을 출력한다 
    **2.** 다음 들여쓰기 단계는 일치하지 않는 부분을 지정한다.
    **3.** 마지막 들여쓰기 단계는 일치하지 않는 부분에 대한 정확한 할당 가능성 오류를 출력한다
    > 
    - logSongs : (song: string)⇒ string은 getSongAt : (index:number)⇒ string 할당되도록 제공된 타입이다
    - logSong의song 매개변수는 getSongAt의 index 매개변수로 할당된다
    - song의 string 타입은 index의 number 타입에 할당 할 수 없다.
    
    <aside>
    💡 타입 스크립트에서 여러 줄로 나타나는 오류가 처음에 어려워보일 수 있지만 차근차근 한 줄씩 읽으며 각 부분이 전달하는 내용을 이해하면 점차 오류를 이해할 수 있다.
    
    </aside>
    

# 5.3.1 함수 타입 괄호

- 함수 타입은 다른 타입이 사용되는 모든 곳에 배치가 가능하며 유니언 타입도 포함된다
- 유니언 타입의 애너테이션에서 **함수 반환 위치를 나타내거나 유니언 타입을 감사는 부분을 표시**할 때 괄호를 사용한다.

```tsx
//string | undefined 유니언을 반환하는 함수
let returnsStringOrUndefined : ()=> string | undefined

// undefined나 string을 반환하는 함수 
let returnsStringOrUndefined : (()=> string) | undefined
```

# 5.3.2 매개변수 타입 추론

# 5.3.2 매개변수 타입 추론

- 매개변수로 사용되는 인라인 함수를 포함해 작성한 모든 함수에 매개변수를 선언하는 것은 상당히 번거롭다
- 타입스크립트는 선언된 타입의 위치에 제공된 함수의 매개변수 타입을 유추할 수 있다.
- 함수를 매개변수로 갖는 함수에 인수로 전달된 함수는 해당 매개변수의 타입을 잘 유추 한다.
- 두번째 코드는 song과 index 매개변수가 string , number로 유추 된 것을 알 수 있다.

```tsx
let singer: (song:string)=>string;

singer = function (song){
	return `Singing : ${song.toUpperCase()}!`; //ok
}

const songs =["Call Me", "Jolene", "The Chain"];

//song : string 
//index : number 
songs.forEach((song,index)=>{
	console.log(`${song} is at index ${index}`);
})
```

# 5.3.3 함수 타입 별칭

- 함수 타입에서도 타입 별칭을 사용 할 수 있다.
- 아래 코드와 같이매개변수 타입을 string , 반환 타입을 number 지정한 StringToNumber 타입 별칭을 생성하여 사용 할 수 있다
- 함수 매개변수도 함수 타입을 참조하는 별칭을 사용할 수 있다.

```tsx
type StringToNumber = (input : string) => number;

let stringToNumber : StringToNumber;

stringToNumber = (input) => input.length

stringToNumber => (input) => input.toUpperCase();
// Error : Type 'string' is not assignable to type 'number'

type NumberToString = (input : number) => string;

function usesNumberToString(numberToString : NumberToString){
	console.log(`The string is : ${numberToString(1234)}`)
}

usesNumberToString((input)=> `${input}! Hooray!`);//ok

usesNumberToString((input)=> input*2);
//
//Error : Type 'number' is not assignable to Type 'string'.
```

<aside>
💡 타입 별칭은 특히 함수 타입에 유용하다. 타입 별칭을 이용하면 반복적으로 작성하는 매개변수와 반환 타입을 갖는 코드 공간을 많이 절약 할 수 있다.

</aside>

# 5.4 그 외 반환 타입

## 5.4.1 void 반환 타입

- void 타입은 자바스크립트가 아닌 함수의 반환 타입을 선언하는데 사용하는 타입스크립트의 키워드이다.
- **return 문이 없는 함수**이거나 **반환 하지 않는 return 문을 가진 함수**일 경우 **void**를 사용한다

```tsx
function logSong(song:string : undefined): void{
	if(!song){
		return; //ok
	}
	return true; 
// Error : Type 'boolean' is not assignable to type 'void'.
}
```

- 함수 타입을 void로 선언시 함수에서 반환되는 모든 값은 무시된다.

```tsx
let singLogger: (song: string) => void; 

singLogger = (song) =>{
	console.log(`${songs}`);
}

singLogger("Heart of Glass");
```

- 자바스크립트는 함수의 값이 반환되지 않으면 기본으로 undefined를 반환한다.
- void는 함수의 반환 타입을 무시 한것을 의미하고 undefined는 리터널 값이 반환 된다고 생각하면된다.
- undefined를 함수타입으로 사용하고 void 타입값을 할당하려 하면 에러가 발생한다.

```tsx
function returnsVoid(){
	return;
}

let lazyValue : string | undefined;

lazyValue = returnsVoid();
//error : Type 'void' is not assignable to type 'string | undefined'.
```

## 5.4.2 never 반환 타입

- never 반환 함수는 (의도적으로) 항상 오류르 발생시키거나 무한 루프를 실행하는 함수이다.
- 함수가 절대 반환하지 않도록 의도하려면 명시적 :never 타입 애너테이션을 추가해 해당 함수를 호출한 후 모든 코드가 실행되지 않음을 나타낸다.
- 아래의 코드는 fail함수는 오류만 발생시키므로 param의 타입을 string으로 좁혀서 타입스크립트의 제어 흐름 부석을 도와준다.

```tsx
function fail(message :string):never {
	throw new Error(`Invariant failure : ${message}`)
}

function workWithUnsafeParam(param: unknown){
	if(typof param !=="string"){
		fail(`param should be a string, not ${typeof param}`)
	}
}

param.toUpperCase()//ok
```

<aside>
💡 never는 void와 다르다 void는 아무것도 반환하지 않는 함수를 위한 것이고 never는 절대 반환하지 않는 함수를 위한 것 이다

</aside>

# 5.5 함수 오버로드

- 타입스크립트에서는 같은 이름을 가진 함수를 여러 개 정의할 수 있으며 각 함수는 서로 다른 타입을 가지는 매개변수로 정의해야 한다. 매개변수가 다르고 이름이 동일한 함수를 함수 오버로드라고 한다.
- **오버로드 시그니처**는 함수가 어떤 파라미터 타입들을 다룰것인지 선언 하는거라고 보면된다
- **구현 시그니처**는 각 파라미터 타입에 대응하는 구체적인 코드를 작성한다고 생각 하면된다.
- 아래의 코드는 처음 두줄은 **오버로드 시그니처**이고 세번째 줄은 **구현 시그니처** 코드이다

```tsx
function createDate(timeStamp :number):Date;
function createDate(month :number, day: number, year: number):Date;
function createDate(monthOrTimestamp :number , day?:number, year?:number):Date{
	return day===undefined || year === undefined 
			? new Date(monthOrTimestamp)
			: new Date(year, monthOrTimestamp, day);
};

createDate(554356800);//ok
createDate(7, 27, 1987)//ok

createDate(4,4)//ok
//
//Error : No overload expects 2 arguments, but overloads
// do exist that expect either 1 or 3 arguments.
```

- 타입스크립트를 컴파일해 자바스크립트로 출력하면 다른 타입 시스템 구문 처럼 오버로드 시그니처도 지워진다
- 함수는 자바스크립트 처럼 컴파일된다.

```tsx
function createDate(monthOrTimestamp, day, year){
	return day===undefined || year === undefined 
			? new Date(monthOrTimestamp)
			: new Date(year, monthOrTimestamp, day);
};
```

<aside>
💡 함수 오버로드는 복잡하고 설명하기 어려운 함수 타입에 사용하는 최후의 수단이다. 함수를 단순하게 유지하고 가능하면 함수 오버로드를 사용하지 않는 것이 좋습니다.

</aside>

# 5.5.1 호출 시그니처 호환성

- **오버로드 시그니처**를 사용 시 **구현 시그니처**에서 **선언한 매개변수 타입과 반환 타입과 동일하게 선언**하여 사용해야한다.
- 아래의 코드를 보면 첫번째, 두번째 **오버로드 시그니처**는 **구현 시그니처**의 매개변수 타입 반환 타입이 동일하여 호환 된다
- 세번째 **오버로드 시그니처**는 매개변수 타입이 동일 하지 않아 타입스크립트에서 에러를 발생 시킨다.

```tsx
function format(data : string): string //ok
function format(data : string, needle: string, haystack: string): string//ok

function format(getData: ()=> string): string 
//
// Error : This overload signature is not compatiblewith its implementation 
// signature

function format(data: string, needle?: string, haystack?: string){
	return needl && haystack ? data.replace(needle, haystack) : data;
}
```
