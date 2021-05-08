### DOM(Document Object Model)은 웹사이트를 유저와 상호작용할 수 있도록 만들기 위해 필수적인 부분이다.
- DOM은 프로그래밍 언어가 웹사이트의 내용(content), 구조(structure) 그리고 스타일을 조작할 수 있게 만들어주는 인터페이스이다.
- 웹사이트는 액션(action)을 취한다. 사용자가 불완전한 형태의 폼을 제출했을 때 에러를 보여주고 네비게이션 메뉴를 토글했을 때는 이미지를 보여주는 것과 같이 화면을 전환하는데, 이러한 일들은 자바스크립트에서 DOM을 조작한 결과이다. 

# DOM
- 웹사이트는 HTML Document라는 것을 포함한다. 웹사이트를 보기 위해 사용하는 브라우저는 HTML과 CSS를 해석하는 프로그램이다. 그리고 style, content, structure등을 우리가 보는 페이지에 랜더링한다. 
- HTML과 CSS의 structure와 style을 파싱하기 위해 브라우저는 Document Object Model이라 불리는 document의 겉모양을 만든다. 이 모델은 자바스크립트가 오브젝트로서의 웹사이트 document의 content와 elements에 접근할 수 있도록 해준다. 

# Document 객체
- document 객체는 우리가 웹사이트에 접근하고 수정할 수 있는 많은 프로퍼티(properties)와 메소드(methods)를 가진 빌트인 객체이다.

# DOM과 HTML 소스 코드의 차이점
- DOM은 자바스크립트 클라이언트 사이드에 의해 수정된다.
- 브라우저는 소스코드에 존재하는 에러를 자동으로 고친다.

> DOM이 수정되는 과정 
```
  > document.body
```

```html
  // output
  <body>
    <h1> ... </h1>
  <body>
```
- document는 오브젝트이다. body는 '.'으로 접근할 수 있는 document의 프로퍼티이다.
- document.body를 콘솔에  작성하는 것은 body엘리먼트와 그 안에 있는 모든 것들을 출력한다.
- 콘솔에서, 해당 웹페이지의 DOM 객체의 라이브 프로퍼티 일부를 수정할 수 있다.
  - document.body를 콘솔에 타이핑해보면 DOM은 변경되지만, 웹사이트의 소스코드는 변하지 않고 클라이언트 사이드 자바스크립트에 어떠한 영향도 받지 않을 것이다.
  - 페이지를 새로고침하면, 콘솔에 추가했던 새로운 코드는 사라진다. 

