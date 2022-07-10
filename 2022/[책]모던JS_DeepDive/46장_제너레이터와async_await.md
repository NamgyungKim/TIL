# 46장 제너레이터와 async/await

## 46.1 제너레이터란?
ES6에서 도입된 제너레이터는 코드블록 실행을 일시 중지했다가 필요햔 시점에 재개 할 수 있는 특수한 함수이다.  

### 제너레이터와 일반함수의 차이
- 제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있다.
- 제너레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있다.
- 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.

## 46.2 제너레이터 함수의 정의
```js
// 제너레이터 함수 선언
function* genDecFunc () => {
  yield 1;
}
const genArrowFunc = () => {
  yield 1;
}
const obj = {
  * genObjMethod(){
    yield 1
  }
}
```

## 46.3 제너레이터 객체
제너레이터 함수를 호출하면 일반함수처럼 함수 코드블록을 싱행하는 것이 아니라 제너레이터 객체를 생성해 반환한다. 제너레이터 함수가 반환한 제너레이터 객체는 이터러블이면서 동시에 이터레이터다. 
|메서드|설명|
|---|---|
|next|제너레이터 함수의 yield 표현식까지 코드블록을 실행시키고 yield된 값을 value프로퍼티 값으로 ,false를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.|
|return|인수로 전달받은 값을 value 프로퍼티값으로, true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.|
|throw|인수로 전달받은 에러를 발생시키고 undefined를 value 프로퍼티 값으로, true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.|

```js
function* getFunc(){
  try{
    yield 1;
    yield 2;
    yield 3;
  } catch (e) {
    console.error(e)
  }
}

const generator = getFunc()

console.log(generator.next()) // { value: 1,done: false }
console.log(generator.return('End')) // { value: 'End', done: true }
console.log(generator.throw('Error')) // { value: undefined, done: true }
```

## 46.6 async/await
제너레이터로 비동기 처리를 구현할 수 있지만 코드가 장황해지고 가독성도 나빠진다.  
ES8에서는 async/await으로 간단히 비동기 처리가 가능해졌다.  
```js
const fetch = require('node-fetch')

async function fetchTodo(){
  const baseUrl = 'https:// ...'
  try{
    const response = await fetch(baseUrl) 
    const todo = await response.json()
    console.log(todo)
  } catch (err) {
    console.error(err)
  }
}

fetchTodo()
```
이처럼 try... catch 문을 사용하면 에러 처리가 가능하다.