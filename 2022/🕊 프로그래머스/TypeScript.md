# ✨ 1. TS 소개

### 장점
- js에 Type을 지정할 수 있다.
- 안정성: 컴파일 단계에서 미리 오류를 감지할 수 있다.
- 가독성: 타입을 보고 무엇을 하는지 미리 알 수 있다. 

### 단점
- 초기설정을 해야한다.
- 스크립트 언어의 유연성이 낮아진다. 
- 컴파일 시간이 길어질 수 있다.  

<br>

## 1. 타임 주석과 타입추론
: 타입 주석은 변수, 상수 혹은 변환 값이 무슨 타입인지 나타내는 것을 의미한다.
타입 추론은 해당 변수가 어떤 타입인지 추론하는 것 , 생략하면 컴파일 타임에 알아낸다.  

```ts
// 타입주석
let a:number = 1
let b = 2
let c: boolean: true
let d: string: 'TS'
let f: { a: 1 }
let h: number[] : [1,2,3]
let i: 'good' = 'good'
let g: any = 3

function add (a: number, b:number):number{
  return a+b
}
```

<br>

## 2. 인터페이스 
: 객체의 타입을 정의하는 방법.

```ts
interface Company{
  name: string,
  age: number,
  address?: string // 선택속성(Optional)
}

const cobalt: Company{
  name: 'Cobalt, Inc',
  age: 3,
  address: 'Seoul'
}

const person: { // 익명 인터페이스
  name: string,
  age?: number
} = {
  name: 'Kim Name',
  age: 30
}
```

## 3. tuple
: 배열을 Tuple로 이용하는 방법

```ts
const tuple: [string, number] = ['Kim Name', 100]
```

<br>

## 4. enum
: 열거형을 사용하는 방법

```ts
enum Color {
  RED = 'red',
  BLUE = 'blue',
  GREEN = 'green'
}

const color = Color.BLUE
color blue
```

<br>

## 5. 대수 타입
: 여러 자료형의 값을 가질 수 있게하는 방법
합집합 타입과 교집합 타입이 있다.

```ts
let numOrStr : num | string = 1;
numOrStr = 'str'

let numAndStr : num & string = ''; // 원시타입에서는 사용 불가

interface Name {
  name: string;
}

interface Age {
  age: string;
}

let namgyung: Name & Age = {
  name: 'namgyung',
  age: 23
}

type Person = Name & Age;
let julia: Person = {
  name: 'julia',
  age: 34
}
```

<br>

## 6. Optional
: ES 2021에도 추가된 기능

```ts
interface Post {
  title: string,
  content: string
}

interface ResponseData {
  post?: Post;
  message?: string;
  status: number
}

const response: ResponseData[] = [
  {
    post: {
      title: 'Hello',
      content: 'How are you?'
    },
    status: 200
  },
  {
    message: 'Error',
    status: 500
  }
]

console.log(response[1].post?.title) // 데이터가 없다면 자동으로 undefined를 반환
console.log(response[1].post!.title) // 값이 무조건 있다는 가정으로
```

7. Generic
: 하나의 인터페이스로 여러 타입을 이용할 수 있게하는 방법

```ts
interface Value<T> {
  value: T
}

const value: Value<string> = {
  value: 1
}

function toString<T>(a: T):string {
  return `${a}`
}

console.log(toString('5'))
```

8. Partial, Required, Pick, Omit
: 기존 interface를 재활용할 수 있게 만든다.

```ts
interface User {
  id: number;
  name: string;
  age: number;
  address: string;
  createAt?: string;
  updateAt?: string;
}

// Partial: 모든 필드가 Optional이 된다.  
const partial: Partial<User> = {}

// 모든 필드가 Required가 된다.
const required: Required<User> = {
  id: 1,
  name: 'KNK',
  age: 12,
  address: 'Seoul',
  createdAt: '',
  updateAt: ''
}

// Pick : 특정 필드만 골라서 사용할 수 있다.
const pick: Pick<User, 'name' | 'age'> = {
  name: '',
  age: 34
}

// Omit: 특정 필드만 빼고 사용할 수 있다.  
const omit: Omit<User, 'id' | 'address' | 'createdAt' | 'updatedAt'> ={
  name: '',
  age: 34
}

// 혼합변수
const mixed: Omit<User, 'id' | 'address' | 'age' | 'createdAt' | 'updatedAt' & Pick<Partial<User>,'address' | 'age'>> = {
  name: '',
}

```

<br> 

9. extends
: 특정 인터페이스를 상속받아 인터페이스를 확장할 수 있다.  

```ts
interface Time {
  hour: number;
  minuit: number;
  second: number;
}

interface DateTime extends Time {
  year: number;
  month: number;
  day: number;
}

interface OffsetDateTime extends DateTime {
  offset: number;
}

interface ZonedDateTime extends DateTime {
  zoneId: string
}

interface TimeFormat extends Pick<Time, 'hour' | 'minuit'> {
  ampm: 'am'|'pm'
}

const timeFormat: TimeFormat = {
  hour: 10,
  minute: 30,
  ampm: 'am'
}
```

