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
- 함수가 new와 함께 호출되었을 때는 묵시적, 명시적 또는 하드 바인딩을 신경쓰지 않는다. 이 때는 그냥 새로운 인스턴스인 새로운 컨텍스트를 만들어낸다.

```javascript
  function foo(something) {
    this.a = something;
  }
  
  var obj1 = {};
  
  var bar = foo.bind(obj1);
  bar(2);
  console.log(obj1.a); // 2
  
  var baz = new bar(3);
  console.log(obj1.a); // 2
  console.log(bar.a); // 3
```
> 위에서 bar변수를 obj1로 바인딩 하였고, new 키워드 없이는 바인딩된대로 잘 동작하였으나, new 키워드가 붙은 이후에는 새로운 컨텍스트를 만들었다. 

# API 호출
- 때때로, 라이브러리나 헬퍼오브젝트를 사용한다. (Ajax, envet handling, etc.. ) 그리고 전달된 콜백을 호출한다. 이러한 경우 this의 동작을 주의해야 한다.
```javascript
  myObject = {
    myMethod: function() {
      helperObject.doSomethingCool('superCool',
        this.onSomethingCoolDone);
      },
      
      onSomethingCoolDone: function() {
        /// Only god knows what is "this" here
      }
  };
```
- 'this.onSomethingCoolDone'을 콜백으로 넘겼기 때문에 스코프가 그 메소드를 참조하고 있다고 생각할 수도 있다.
- 이 부분을 고치기 위해 몇 가지 방법이 있다.
  - 주로 라이브러리들은 또 다른 파라미터를 제공한다. 그곳에 다시 가져오길 원하는 스코프를 전달할 수 있다.
  ```javascript
    myObject = {
      myMethod: function() {
        helperObject.doSomethingCool('superCool', this.onSomethingCoolDone, this);
      },
      
      onSomethingCoolDone: function() {
        /// Now everybody know that "this" === myObject
      }
    }
  ```
  - 원하는 스코프를 바인드 할 수도 있다.
  ```javascript
    myObject = {
      myMethod: function () {
        helperObject.doSomethingCool('superCool', this.onSomethingCoolDone.bind(this));
      },
      onSomethingCoolDone: function() {
        // Now everybody know that "this" === myObject
      }
    };
  ```
  - 클로저를 만들고 `this`를 `me`에 캐시할 수도 있다.
  ```javascript
    myObject = {
      meMethod: function () {
        var me = this;
        
        helperObject.doSomethingCool('superCool', function() {
          // Only god knows what is "this" here, but we have access to "me"
        });
      }
    };
  ```

# call(), apply(), bind()
- 자바스크립트에서 함수들은 오브젝트이고 `call(), apply(), bind()` 3개의 메소드는 함수의 호출을 제어하기 위해 사용된다.
- 함수를 즉시 호출하기 위해서 `call(), apply()` 메소드를 사용할 수 있다. 
- `bind()`는 함수가 나중에 실행됐을 때도 원본 함수를 호출할 때 갖는 올바른 컨텍스트(this)가 bind된 함수를 반환한다. 
  - `bind()`는 특정 이벤트에서 함수가 나중에 호출될 필요가 있을 때 유용하다.

## call() or Function.prototype.call()
```javascript
  // Demo with javascript .call()
  
  var obj = { name: 'Niladri'};
  
  var greeting = function(a, b, c) {
    return 'welcome ' + this.name + ' to ' + a + ' ' + b + ' in ' + c;
  };
  
  console.log(greeting.call(obj, 'Newtown', 'KOLKATA', 'WB');
  // welcome Niladri to Newtown KOLKATA in WB
```
- `call()`메소드의 첫번 째 파라미터는 함수가 호출되는 순간 'this' 오브젝트 값을 세팅한다. 위 코드의 경우 obj가 this 오브젝트이다.
- 나머지 파라미터들은  실제 함수의 인자들이다.

## apply() or Function.prototype.apply()
```javascript
  // Demo with javascript .apply()
  
  var obj = { name: 'Niladri'};
  
  var greeting = function(a, b, c) {
    return 'welcome ' + this.name + ' to ' + a + ' ' + b + ' in ' + c;
  };
  
  // array of arguments to the actual function
  var args = ['Newtown', 'KOLKATA', 'WB'];
  console.log('Output using .apply() below');
  console.log(greeting.apply(obj, args);
  // Output using .apply() below
  // welcome Niladri to Newtown KOLKATA in WB
```
- 첫번 째 파라미터는 함수가 호출되는 순간 "this"의 값을 세팅한다. 위 코드의 경우 obj 오브젝트이다.
- `apply()` 메소드가 `call()` 메소드와 다른 점은 두번 째 파라미터에서 실제 함수의 인자를 배열로 받는다는 것이다.

## bind() or Function.prototype.bind()
```javascript
  //Use .bind() javascript

  var obj = {name:"Niladri"};

  var greeting = function(a,b,c){
      return "welcome "+this.name+" to "+a+" "+b+" in "+c;
  };
  
  // creates a bound function that has same body and parameters
  var bound = greeting.bind(obj);
  
  console.dir(bound); // returns a function
  console.log('Output using .bind() below');
  console.log(bound('Newtown', KOLKATA', 'WB'));
  // Output using .bind() below
  // welcome Niladri to Newtown KOLKATA in WB
```
- 첫번 째 파라미터는 함수가 호출될 때 타겟 함수에서 'this'의 값을 세팅하는 부분이다.
- 함수가 new 연산자를 이용하여 생성되었을 때는 바인드 시킨 this 값이 무시된다. 나머지 파라미터들은 인자로 잘 넘겨진다.
  
