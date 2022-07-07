# 43장 Ajax

## 43.1 Ajax란?
Ajax란 js를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식을 말한다.  
WebAPI인 XMLHttpRequest 객체를 기반으로 동작한다. 

### Ajax이전
  - html문서 전체를 서버로 부터 전송을 받았다. 그렇기 때문에 택스트 하나 변경되는데 주변의 모든 코드들을 다시 전송 받기 때문에 불필요한 데이터 통신이 발생했다.   
  - 페이지가 변경되며 화면전환과정에서 깜빡거리는 현상이 발생했다.
  - 서버통신이 동기적으로 동작해 서버로부터 응답이 있을 때까지 블로킹되었다.   

### Ajax를 사용하며..
  - 필요한부분만 갱신하게 되므로 불필요한 데이터 통신이 발생하지 않는다. 
  - 변경이 필요없는부분은 다시 렌더링되지 않는다.
  - 서버 통신이 비동기적으로 동작하기 때문에 블로킹 현상이 발생하지 않는다.

## 43.2 JSON
JSON은 클라이언트와 서버간 HTTP 통신을 위한 텍스트 데이터 포멧이다.  
대부분의 프로그래밍언어에서 사용할 수 있다. 

### JSON 표기 방식
JSON은 JS의 객체 리터럴과 유사한 포멧 을 갖고 있다. 
키와 text는 반드시 큰따옴표로 묶어야한다.
```json
{
  "id":"534242",
  "name":"kim",
  "post":{
    "title":"JSON의 형식",
    "content":"JSON은 클라이언트와 서버간 HTTP 통신을 위한 텍스트 데이터 포멧이다."
  },
  "like": 45,
}
```
### JSON.stringify
서버로 객체를 전송하기 위해서는 객체를 문자열화 해야한다.  
`JSON.stringify`는 객체를 JSON 포멧의 문자열로 변환해준다.  

### JSON.parse
`JSON.parse`는 서버로 부터 받아온 JSON포맷을 객체로 변환시켜준다. 

> 직렬화: 네트워크를 통해 다른 곳으로 전송할 수 있는 형식이나 파일에 저장할 수 있는 형식으로 객체를 변환하는 것
> 역직렬화: 데이터를 본래의 객체로 되돌리는 변환  

출처: https://cmang9.tistory.com/97 [My Life is...:티스토리]

## 43.3 XMLHttpRequest
html의 a태그 처럼 js에서 HTTP 요청을 전송하기위해 사용된다.  
`XMLHttpRequest`객체는 HTTP 요청과 수신을 위한 다양한 메서드와 프로퍼티를 제공한다.

### XMLHttpRequest 객체 생성
XMLHttpRequest 객체는 생성자 함수를 호출해 생성한다.  
브라우저에서 제공하는 WebAPI이므로 브라우저 환경에서만 정상적으로 실행된다.
```js
const xhr = new XMLHttpRequest()
```

### HTTP 요청 전송

HTTP 요청을 전송하는 경우 다음 순서를 따른다. 
1. `XMLHttpRequest.open` 메서드로 HTTP요청을 초기화 한다.
2. 필요에따라 `XMLHttpRequest.setRequestHeader`메서드로 특정 HTTP요청의 헤더 값을 설정한다. 
3. `XMLHttpRequest.send`메서드로 HTTP요청을 전송한다.

```js
const xhr = new XMLHttpRequest()

xhr.open('GET','/users')

xhr.setRequestHeader('content-type','application/json')

xhr.send()
```
