# Interfaces vs type

인터페이스는 오직 오브젝트의 모양을 특정해주기 위한 것이다. 
인터페이스를 이용해 class의 모양을 알려준다는 점에서 유용하다.
interfaces는 객체지향 프로그래밍의 개념을 활용해 디자인되었고,  
type은 더 유연하다.

1. 상속이 가능하다
```ts
interface User{
  name: string
}

interface Player = User & {

} 
const knk : Player ={
  name: 'knk'
}
```

2. property 축적이 가능하다
```ts
interface User{
  name: string
}

interface User{ 
  lastName: string
}

interface User{
  health: number
}

const knk: User = {
  name: 'knk',
  lastName: 'kim',
  health: 10
}
```

추상화가 아닌 Interface를 사용해야하는 이유
- 아래 ts를 변환하면 Class User 가 컴파일 되는 반변, interface는 컴파일하면 그대로 사라진다.

```ts
abstract class User{
  constructor (
    protected firstName:string,
    protected lastName: string
  ){}
  abstract sayHi(name:string):string
  abstract fullName():string
}

// 추상화는 인스턴스를 만드는 것을 허용하지 않는다.
// new User는 사용할 수 없다.
class Player extends User{
  fullName(){
    return `${this.firstName} ${this.lastName}`  
  }
  sayHi(name:string){
    return `Hello ${name}. My name is ${this.FullName()}`
  }
}
```
아래가 interface로 변환후 
```ts
interface User{
  firstName: string,
  lastName: string,
  sayHi(name:string): string,
  fullName(): string
}

interface Human {
  health:number
}

// 아래 extends를 사용하면 js로 바뀐다.
class Player implements User,Human{
  constructor(
    public firstName: string,
    public lastName: string,
    public health:number
  )
   fullName(){
    return `${this.firstName} ${this.lastName}`  
  }
  sayHi(name:string){
    return `Hello ${name}. My name is ${this.FullName()}`
  }
}
```