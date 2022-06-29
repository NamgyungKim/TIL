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