# 39장 DOM

## 39.1 노드
### HTML 요소와 노드 객체
`<div class="message">Hello!</div>`
html은 렌더링엔진에 의해 파싱되며 DOM을 구성하는 요소 노드 객체로 변환된다.  
이때, 요소노드`<div>`, 어트리뷰트 노드`class="message"`, 텍스트 노드`Hello`와 같이 쪼개져서 노드 객체를 이루게 된다.  
이때 이 노드들의 부자 관계를 반영해 트리 자료구조를 이루게 되는데 이를 DOM이라 한다. 

### 노드 객체의 타입
- 문서 노드: DOM의 최상위에 존재하는 루트 노드로 document객체를 가리킨다. 이는 window의 document프로퍼팉에 바인딩 되어 있다.  
- 요소 노드 : html의 요소를 가리키는 객체이다. (div, p, span, h1/h2/h3/h4/h5 ...)
- 어트리뷰트 노드 : 요소노드의 어트리뷰트를 가리키는 객체이다. 어트리뷰트 노드는 지정된 요소노드에만 연결되어있다.
- 텍스트 노드 : 텍스트노드는 자식 노드를 갖을 수 없는 리프노드이다. 
이 외에 comment노드(주석), DOCTYPE을 위한 DocumentType노드 등 총 12개의 노드 타입이 있다. 

### 노드 객체의 상속 구조
모든 노드객체는 Object, EventTarget, Node 인터페이스를 상속 받는다. 추가로 문서노드는 Document, HTMLDocument 인터페이스를 상속받고, 어트리뷰트 노드는 Attr, 텍스트 노드는 CharacterDate 인터페이스를 각각 상속 받는다.  
즉 노드객체는 프로토타입 체인에 있는 모든 프로토 타입의 프로퍼티나 메서드를 상속받아 사용할 수 있다.  

|input 요소노드 객체의 특성|프로토타입을 제공하는 객체|
|---|---|
|객체|Object|
|이벤트를 발생시키는 객체|EventTarget|
|트리 자료구조의 노드 객체|Node|
|브라우저가 렌더링할 수 있는 웹문서의 요소(HTML,XML,SVG)를 표현하는 객체|Element|
|웹 문서의 요소 중에서 HTML요소를 표현하는 객체|HTMLElement|
|HTML요소 중에서 input 요소를 표현하는 객체|HTMLInputElement|

<br>

## 39.2 요소 노드 취득
DOM을 조작하기 위해서는 요소 노드를 취득해야한다. 
이를 위해 DOM은 요소노드를 취득할 수 있는 다양한 메서드를 제공한다.

### id를 이용한 요소 노드 취득
- `document.getElementById('id')`
- id는 html문서내에서 유일한 값이여야한다.  
- 만약 중복된 값이 있어도 오류를 발생하지는 않지만, 가장 첫번째값만 반환된다.  
- 만약 선택한 값이 없을 경우 null을 반환한다.  

### 태그를 이요한 요소 노드 취득
- `document.getElementsByTagName('tag')`
- 메서드 이름에 s가 붙은대로 여러개의 노드 객체를 갖는 DOM객체를 반환한다.  
- HTMLCollection객체는 배열객체이면서 이터러블 이다. 
- 인수로 '*'을 넣을 경우 모든 html문서의 요소를 취득하게된다.  
- 만약 선택한 값이 없을 경우 빈HTMLCollection 객체를 반환한다. 


### Class 를 이용한 요소노트 취득
- `document.getElementsByClassName('class')`
- 메서드 이름에 s가 붙은대로 여러개의 노드 객체를 갖는 DOM객체를 반환한다.  
- HTMLCollection객체는 배열객체이면서 이터러블 이다. 
- 만약 선택한 값이 없을 경우 빈HTMLCollection 객체를 반환한다. 

### CSS 선택자를 이용한 요소노드 취득
- `document.querySelector('#id')`
  : 선택한 요소중 인자 첫번째노드만 반환


- `document.querySelectorAll('.class')`  
  : 선택한 모든 요소노드를 반환  
  NodeList객체 반환

```css
* {...}
p {...}
.class {...}
#id {...}
input[type=text] {...}
div p {...}
div > p {...}
/* p바로뒤 ul태그 */
p + ul {...} 
/* p뒤 ul태그 */
p ~ ul {...}
a:hover {...}
p::before {...}
```
> CSS선택자인 querySelector는 getElementBy...보다 다소 느리다고 알려져 있다.   
> 하지만 CSS선택자 문법을 사용하면 좀 더 구체적인 조건으로 노드를 취득할 수 있고 일괄된 방식으로 노드를 취득할 수 있다는 장점이 있다.  
> 따라서, id 요소노드를 취득하는 getElementById를 사용할때를 제외하고는 querySelector 메서드 사용을 권장한다.

### 특정 요소노트를 취득할 수 있는지 확인
`document.matches('#id')`는 특정요소 노드를 취득할 수 있는지 여부를 확인 할 수 있다.  
해당 여부에 따라서 boolean으로 값이 넘어온다.

### HTMLCollection과 NodeList 
HTMLCollection과 NodeList는 여러개의 값을 받아오기위한 DOM 컬렉션이다.  
유사배열 객체이며, 이터러블이다. 따라서 `for... of`문으로 순회가 가능하다.


<br>

## 39.3 노드 탐색
<br>

## 39.4 노드 정보 취득
<br>

## 39.5 요소 노드의 텍스트 조작
<br>

## 39.6 DOM 조작
<br>

## 39.7 어트리뷰트
<br>

## 39.8 스타일
<br>

## 39.9 DOM표준
<br>

