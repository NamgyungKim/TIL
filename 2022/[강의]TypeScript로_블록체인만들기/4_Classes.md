# Classes

js에서는 private, public을 제공하지 않는다.  
그래서 ts에서 작성된 private, public이 컴파일 후 반영되지는 않지만 ts로 작성시에 적용된다.
```ts
class Player {
    constructor (
        private firstName: string,
        private lastName: string,
        public nickName: string
    ){}
}
const knk = new Player('namgyung','kim','knk')
console.log(knk.nickName)
```
이렇게 `private`으로 작성하면 자식요소들도 접근이 불가능하다. 
하지만 자식요소에게는 접근이 가능하도록하려면`protected`를 써주면 된다.

```ts
abstract class User {
    constructor (
        private firstName: string,
        private lastName: string,
        protected nickName: string
    ){}

    abstract getNickName():void //추상메서드

    getFullName(){
        return `${this.firstName} ${this.lastName}`
    }
}

class Player extends User {
    getNickName(){
        this.nickName
    }
}
```

> 추상메서드란 아직 구현되지 않은 메소드이다.  
> 메서드의 이름, type을 정의 해야한다.  
> 구현은 상속받는 클래스에서 이루어진다.

## Dictionary(예시1)
```ts
type Words = {
    [key:string]: string // 객체로 들어올 아이템들의 type지정
}

class Dic {
    private words: Words
    constructor(){
        this.words = {}  //초기화
    }
    add(word:Word){
        if(this.words[word.term] === undefined){
            this.words[word.term] = word.def
        }
    }
    def(term:string){
        return this.words[term]
    }
}

class Word {
    constructor(
        public term:string,
        public def: string
    ){}
}
```
