

# TypeScript 개요

type을 지정하는 방법은 2가지가 있다. 하나는 ts가 type을 추론하도록 하는 방법과 직접 type을 명시 하는 것이다.

## type 추론
```ts
let num = 123 // 여기에서 num은 숫자라고 ts에서 추로한다. 
num = '123' // Error : Type 'number' is not assignable to type 'string'.
let numArr = [1,2,3]
numArr.push('4') // error
```

위에서 TS가 추론한 것 과 다른 type이 num에 들어가면 오류메시지가 뜬다. 

## type 작성
```ts
let str: string = 'abc'
let numArr: number[] = []
```
위와 같이 type을 지정할 수도 있다. 
하지만 변수생성시 TS가 추론하도록 하는게 더 좋다.

## Type

object같은 경우 `person: object`라고 써주는 것이 아니라 아래와 같이 object의 요소에대한 모든 type을 작성해줘야한다.
```ts
const person :{
  name?: string, // 옵션값
  age: number // 필수값
} = {
  name: 'knk',
  age: 12
}

// 아래의 예제처럼 type Aliases를 지정해줄 수 있다.
type person = {
  name?: string,
  age: number
}

const person1: person={
  name: 'knk',
  age: 12
}

```

함수에서 type을 작성할 경우  
변수의 type과 결과 값에대한 type을 작성해야한다.
```ts
function addNumber(a:number,b:number):number{
    return a+b
}
```

## readOnly

readOnly로 지정해둔 값은 수정할 수 없다.  
수정을 시도할 경우 오류가 난다.   
```ts
type person = {
  readonly name?: string,
  age: number
}

const person1: person={
  name: 'knk',
  age: 12
}

person1.name = '234'
// Error : Cannot assign to 'name' because it is a read-only property.

const arr: readonly string[] = ['1','2','3']
arr.push('12') // Error
```

## Tuple

배열 생성시 각 배열 위치별로 type을 지정해줄 수 있다. 
```ts
const arr:[number,boolean,string] = [23,false,'문자']
```

## any
any에는 아무타입이나 올 수있다.  
any는 모든 TS의 보호장치들을 비활성화 시키므로 되도록 사용하지 않는 것이 좋다.

## unknown 
아직 변수에 어떤 type이 올 지 모르는 경우에 type에 unknown을 작성한다. 
이후 해당변수를 사용하기위해서는 type체크를 한 후 사용할 수 있게된다.
```ts
let a : unknown;

if(typeof a=== 'number'){
    let b = a+1
}
```

## void
함수에서 return 값이 없는 경우 void라 한다. 
return 값이 없을 경우, `function add():void`라고 작성해주지 않아도 된다.

## never
함수에 return 타입으로 사용된다.  
return type으로 never가 사용될 경우, 항상 오류를 출력하거나 리턴값을 내보내지 않음을 의미한다.

```ts
function hello(message:string|number){
    if (typeof message === 'string'){
        message // string type
     }else if(typeof message === 'number'){
        message // number type
    } else {
        message // never type 값이 제대로 들어왔으면 실행되면 안된다.
    }
}
```