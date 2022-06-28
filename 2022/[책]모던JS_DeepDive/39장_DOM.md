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
모든 노드객체는 Object, EventTarget, Node 인터페이스를 상속 받는다.  
추가로 문서노드는 Document, HTMLDocument 인터페이스를 상속받고, 어트리뷰트 노드는 Attr, 텍스트 노드는 CharacterDate 인터페이스를 각각 상속 받는다.  
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
노드를 취득한 다음 그 노드를 기점으로 DOM트리의 노드를 옮겨다니며 부모, 형제, 자식 노드 등을 탐색해 나간다.  
이때 DOM트리를 탐색할 수 있도록 Node,Element 인터페이스는 트리 탐색 프로퍼티를 제공한다.  
노트 탐색 프로퍼티는 setter없이 getter만 존재하여 참조만 가능한 **읽기 전용 접근자** 프로퍼티이다. 

### 공백 텍스트 노드
스페이스, 탭, 줄바꿈 등 공백 문자는 텍스트 노드를 생성한다.  
만약 공백없이 작성한다면 가독성에 좋지 않으므로 권장하지 않는다.
```html
<ul id="number"><li class="1">2</li><li class="2">2</li><li class="3">3</li></ul>
```

### 자식 노드 탐색
|프로퍼티|설명|
|-------|-----|
|Node.childNode|요소 노드 뿐아니라 텍스트 노드 포함|
|Element.children|HTMLCollection에 담아 반환한다. 여기에는 텍스트 노드가 포함되지 않는다.|
|Node.firstChild|첫번째 자식노드 반환|
|Element.lastChild|마지막 자식노드 반환|
|Node.firstElementChild|첫번째 자식요소노드 반환|
|Element.lastElementChild|마지막 자식요소노드 반환|

### 자식 노드 존재확인
|프로퍼티|설명|
|-------|-----|
|Node.hasChildNodes|자식이 있는지 boolean으로 반환|
|Node.childElementCount|자식노드중 텍스트 노드가 아닌 요소노드가 존재하는지 확인.|
(Node.children.length 자식노드중 텍스트 노드가 아닌 요소노드가 존재하는지 확인.)
### 부모 노드 탐색
|프로퍼티|설명|
|-------|-----|
|Node.parentNode|부모노드 탐색|
### 형제 노드 탐색
|프로퍼티|설명|
|-------|-----|
|Node.previousSibling|자신 **이전의 형제노드**를 반환한다. 노드는 요소노드 뿐아니라 텍스트 노드 일수도 있다.|
|Node.nextSibling|자신 **다음 형제 노드**를 탐색해 반환한다. 노드는 요소노드 뿐아니라 텍스트 노드 일수도 있다.|
|Element.previousElementSibling|자신 **이전의 형제요소노드**를 탐색하여 반환한다.|
|Element.nextElementSibling|자신의 **다음 형제요소 노드**를 탐색하여 반환한다. |

<br>

## ✨ 39.4 노드 정보 취득
|프로퍼티|설명|
|-------|-----|
|Node.nodeType|요소 노드타입: 1,<br> 텍스트 노드타입: 3 <br> 문서노드타입: 9 <br>각 해당하는 상수를 반환한다.|
|Node.nodeName|요소노드: ul, li 등 <br> 텍스트노드: #text <br> 문서노드: #document <br>를 반환한다.|

<br>

## 39.5 요소 노드의 텍스트 조작
요소노드의 텍스트를 조작하기 위해서는 setter, getter를 모두 존재하는 접근자 프로퍼티를 사용해야한다.

### nodeValue
텍스트 노드를 취득한 뒤 nodeValue를 이용해 값을 변경할 수 있다.
`$textNode.nodeValue = 'ABC'`
### textContent
textContent메서드를 이용하면 요소노드의 컨텐츠영역 내의 텍스트를 모두 반환한다.   
이때 마크업문법을 넣어도 마크업이 파싱되지 않는다.  

> textContent와 유사한 동작을하는 innerText라는 프로퍼티가 있다. 
> 하지만 다음과 같은 이유로 사용을 권장하지 않는다.
> - `visibility:hidden`과같은 비표기 요소의 텍스트를 반환하지 않는다.
> - innerText는 CSS를 고려해야함으로 textContent보다 느리다

<br>

## 39.6 DOM 조작
: DOM조작은 DOM에 노드를 생성, 삭제, 변경 하는 것을 말한다.

### innerHTML
textContent는 마크업은 무시하고 텍스트만 반환하지만 innerHTML은 마크업이 포함된 문자열을 그대로 변환한다.   
innerHTML은 삽윕위치를 지정할 수 없고, 문자열을 할당하는 요소노드의 모든 자식 노드를 제거해 할당한다. 

- 장점: 구현이 간단하고 직관적이다.
- 단점: 크로스 사이트 스크립팅 공격에 취약하다. 

### insertAdjacentHTML 메서드
insertAdjacentHTML는 기존의 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입할 수 있다.  
첫번째 인수로 `beforebegin`,`afterbegin`,`beforeend`,`afterend` 이렇게 4가지 위치를 선택해 할당할 수 있고, 
두번째 인수로는 html마크업문자를 전달할 수 있다.  

하지만 innerHTML과 마찬가지로 크로스 사이트 스크립팅 공격에 취약하다는 점은 동일하다.

```html
<!-- beforebegin -->
<div>
  <!-- afterbegin -->
  text
  <!-- beforeend -->
</div>
<!-- afterend -->
```


<br>

## 39.7 어트리뷰트
<br>

## 39.8 스타일
<br>

## 39.9 DOM표준
<br>

