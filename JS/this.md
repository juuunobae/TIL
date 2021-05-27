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
- 코드 안의 myObject는 myMethod라는 프로퍼티를 갖고, 이 프로퍼티는 myMethod 함수를 가리킨다. myMethod 함수가 글로벌 스코프로부터 호출됐을 때, `this`는 window object를 참조하고, myObject의 메소드로서 호출됐을 때는 , `this`가 myObject를 참조한다.
```javascript
  myObject.myMethod(); // this === myObject
  myMethod(); // this === window
```
> 이러한 형식은 묵시적 바인딩이라 불린다.

# 명시적 바인딩
- 함수에 명시적으로 컨텍스트를 바인딩 하는 것, 주로 `call()` 메소드와 `apply()` 메소드에 의해 이루어진다.

```javascript
  var myMethod = function () {
    console.log(this);
  };
  
  var myObject = {
    myMethod: myMethod
  };
  
  myMethod() // this === window
  myMethod.call(myObject, args1, args2, ...) // this === myObject
  myMethod.apply(myObject, [array of args]) // this === myObject
```
- 명시적 바인딩은 묵시적 바인딩보다 우위를 갖는다.
```javascript
  var myMethod = function () {
    console.log(this);
  };
  
  var obj1 = {
    a: 2, 
    myMethod: myMethod
  };
  
  
  var obj2 = {
    a: 3,
    myMethod: myMethod
  };
  
  obj1.myMethod(); // 2
  obj2.myMethod(); // 3
  
  obj1.myMethod.call(obj2); // 3
  obj2.myMethod.call(obj1); // 2
```

# 하드 바인딩
- 하드 바인딩은 `bind()`로 가능하다. `bind()` 메소드는 우리가 지정한 `this` 컨텍스트를 가진 기존 함수를 불러오기 위해 하드코딩된 새로운 함수를 반환한다.
```javascript
  myMethod = myMethod.bind(myObject);
  myMethod(); // this === myObject
```
- 하드바인딩은 명시적 바인딩보다 우위를 갑는다.
```javascript
  var myMethod = function() {
    console.log(this);
  };
  
  var obj1 = {
    a: 2
  };
  
  var obj2 = {
    a: 3
  };
  
  myMethod = myMethod.bind(obj1); // 2
  myMethod.call(obj2) // 2 명시적 자인딩은 obj2이다, obj1로 하드바인딩 되어있음
```
  
# 'New' 바인딩
```javascript
  function foo(a) {
    tish.a = a;
  }
  
  var bar = new foo(2);
  conosole.log(bar.a); // 2
```

- 새로운 new 인스턴스를 참조하는 함수가 호출되었을 때, `this`가 만들어진다.
- 함수가  
