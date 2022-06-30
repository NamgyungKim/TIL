# Function

## call signature

TS는 함수를 만들기 전에 함수의 type을 정의해줄 수 있다. 
```ts
type Add = (a:number , b:number) => number
const add:Add = (a, b) => a+b
```

## polymorphism(다양성)

함수 가 여러개의 call signatures를 갖고 있을 때 overloading이 발생된다.  
> overloading이 가능하다는건, 이름은 같지만 매개변수 유형과 반환 유형이 다른 여러 함수를 가질 수 있다. 그러나 매개변수의 수는 동일해야 함을 의미한다.

```ts
type Add = {
    (a:number , b:number): number
    (a:number , b:string): number
}
const add:Add = (a, b) => {
    if(typeof b === 'string')return a
    return a + b
}
```
파라미터 갯수가 다를경우
```ts
type Add = {
    (a:number, b:number):number
    (a:number, b:number, c:number):number
}
const add:Add = (a,b,c?:number) =>{
    if(c) return a+b+c
    return a+b
}
```

> concrete type: number ,boolean, string, void, unknown

## Generics
제네릭은 기본적으로 placeholder를 사용해 작성한 코드 타입기준으로 변경해준다.  
라이브러리를 만들거나, 개발자가 사용할 기능을 개발하는 경우 제네릭이 더 유용하다.  

```ts
type SuperPrint = {
    (arr: number[]):void
    (arr: boolean[]):void
    (arr: string[]):void
}

const superPrint:SuperPrint = (arr)=>{
    arr.forEach(i => console.log(i))
}

superPrint([1,2,3,4,5])
superPrint([true,false,false])
superPrint(['sdf'])
```
위처럼 일일히 type을 정해줄 수 있지만, 제네릭을 통해 더 간편히 코드를 작성할 수 있다.

```ts
// ex1
type SuperPrint = {
    <T>(arr: T[]):void
}
const superPrint:SuperPrint = (arr)=>{
    arr.forEach(i => console.log(i))
}
superPrint([1,2,3,4,5]) // T -> number
superPrint([true,false,false])
superPrint(['sdf',3,4,false])


// ex2
function returnFirstValue<T>(a: T[]){
    return a[0]
}
const a = returnFirstValue<boolean>([true,false,false])


// ex3
type Player<E> = {
    name: string
    extraInfo: E
}

const knk: Player<{age:number}> = {
    name:"knk",
    extraInfo: {
        age: 12
    }
}

// ex4
// Array의 경우 제네릭을 받고 있다.
type A = Array<string>
let a:A = ['a','b']
```

인자가 2개인 경우,
```ts
type SuperPrint = {
    <T,M>(arr: T[], b:M):void
}

const superPrint:SuperPrint = (arr)=>{
    arr.forEach(i => console.log(i))
}

superPrint([1,2,3,4,5], 'm')
```