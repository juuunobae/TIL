# BOM과 DOM
## BOM
- 웹은 기본적으로 웹 브라우저를 통해 서비스된다.
- 브라우저는 html을 읽어들여 사용자에게 보여주는데 이러한 브라우저와 관련된 객체들의 집합을 `브라우저 객체 모델(Browser Object Model, BOM)`이다.
- 브라우저는 BOM을 이용하여 브라우저의 기능들을 수행할 수 있다.

## DOM
- BOM의 하위 객체로써 `Document Object Model`의 약자이며 문서 객체 모델이라고 한다.
- 문서 객체란 `<html>, <body>`등의 태그들, 즉 자바스크립트를 이용하여 수정이 가능한 객체라고 할 수 있다.
- DOM은 브라우저가 자바스크립트를 이용해 웹 페이지를 조작할 수 있도록 제공해주는 요소이고, 그런 조작들을 엄밀히 말하면 원본 html문서를 조작하는 것이 아니라 DOM을 조작하는 것이다.

# 트리구조
- DOM은 `트리구조`로 이루어져 있다. 
- ![DOM 트리구조](https://github.com/juuunobae/TIL/blob/main/Javascript/스크린샷%202021-03-10%20오전%2010.42.09.png)
  - Document Node: 최상위에 존재하며 DOM 트리에 접근하기 위한 Root Node이다.
  - Element Node: h1, div 같은 태그를 가르키는 Node이다.
  - Attribute Node: class, id, href, style 같은 속성에 대한 Node이다.
  - Text Node: `<div>Hello world</div>`에서 태그안에 감싸진 Hello world를 가르키는 Node이다.

# 문서 객체
- 정적인 문서 객체와 동적인 문서 객체 2가지 종류가 있다.

## 정적인 문서 객체
- 원본 html 문서에 있는 객체들

## 동적인 문서 객체
- 자바스크립트의 .createElement메서드로 생성해준 객체들

# DOM은 브라우저에 보이지 않는다.
- DOM은 <html>, <div> 같은 태그라고 하였지만 이것들을 함부러 DOM이라고 단정지으면 안된다.
- 우리가 사용하는 웹페이지는 DOM + CSSOM의 조합인 `렌더트리`라는 것을 보여주는 것이다.
  </br></br>
- `<p style='display:none'>Hello</p>`를 만들게 되면 스타일 속성 때문에 <p>태그를 화면에서 불 수 없다. 하지만 자바스크립트로 `<p>`태그 조작이 가능하다.
- ![DOM, 렌더트리](https://github.com/juuunobae/TIL/blob/main/Javascript/스크린샷%202021-03-10%20오전%2011.41.45.png)
  - `<p>`태그는 자바스크립트로 display: none 속성을 적용했기 때문에 렌더트리에는 보이지 않는다.

# 개발자도구의 Element는 DOM인가
- display none인 태그가 보인다고 해서 DOM이라고 생각할 수도 있지만 DOM은 아니다.
- 개발자 도구에서 가상요소 `(::after, ::before)`가 보여지는데 이들은 DOM이 아닌 CSSOM으로만 이루어져 있다.
- DOM이 아닌 가상요소가 개발자 도구에 보여지기 때문에 개발자 도구는 DOM이 아닌것이다.
- DOM은 자바스크립트를 이용하여 수정이 가능한 객체를 해석하는데 가상요소 after와 before는 자바스크립트로 조작이 불가능하다

# 요약
### DOM은 항상 유효한 html 형식이다.
### JS에 의해 조작가능하여야 한다.
### 가상요소를 포함하지 않는다. (ex: after, before)
### 보이지 않는 요소를 포함한다. (ex: display: none)
### 렌더트리와 DOM은 다르다.
### 개발자 도구의 Element와 DOM은 다르다.
