# this의 개념
- 함수가 만들어졌을 때 뒤에서는 `this`라 불리는 키워드가 만들어진다. `this`는 함수가 동작하는 곳에 있는 오브젝트와 연결해준다.
- `this` 키워드의 값은 그 함수 자체와는 상관이 없다. 함수가 어떻게 불려지는지가 `this`의 값을 결정한다.

# this 컨텍스트
```javascript
  // define a function
  var myFunction = function() {
    console.log(this);
  };
  
  // call it
  myFunction();
```

- `this`는 언제나 전역 스코프의 root를 참조하는 window Object가 된다.
- 스크립트가 strict model(`"use strict"`)내에서 작동하고 있다면, `this`는 undefined일 것이다.

# 오브젝트 리터럴
```javascript
  var myObject = {
    myMethod: function() {
      console.log(this);
    }
  };
```
- 여기서 `this`의 값이 무엇이 들어올지는 모른다.
- `this`키워드의 값은 함수 그 자체와는 상관 없고, 함수가 어떻게 호출 되는지가 `this`의 값을 결정한다.

```javascript
  var myMethod = function() {
    console.log(this);
  };
  
  var myObject = {
    myMethod: myMethod
  };
```
- 코드 안의 myObject는 myMethod라는 프로퍼티를 갖고, 이 프로퍼티는 myMethod 함수를 가리킨다. myMethod 함수가 글로벌 스코프로부터 호출됐을 
