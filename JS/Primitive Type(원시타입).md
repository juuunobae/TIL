### 자바스크립트에는 6가지 종류의 원시 데이터 타입이 있고, 이것들은 객체가 이닌 값 그 자체로 저장이 되는 것들이다.
#### Booleans - `true` or `false`
#### null
#### undfined
#### number
#### string
#### symbol
- 이 6가지를 제외한 것들은 `Object`이다. Object는 키-값 저장소이며, 함수들과 배열들도 포함된다.

# 원시 타입
- 원시 타입은 어떠한 메소드도 붙어있지 않는 특성 때문에 불변적(immutable)속성을 갖는다.
- 변수에 원시 타입을 재할당 할 수 있지만, 변수에 할당되었던 원시 값을 바꾸는게 아니라 새로운 원시타입 값이 들어가는 개념이다.
- 원시타입의 값 자체는 절대 바뀔 수 없다.
```javascript
  'dog' === 'dog'; // true
  14 === 14; // true
  
  {} === {}; // false
  [] === []; // false
  (function() {}) === (function() {}); // false
```
- 원시 타입은 참조(reference)로 저장되는 Object와 다르게 값 그 자체로 저장된다.
- 원시 타입은 같은 값을 저장하고 있기 때문에 true이고, 객체는 값은 같지만 참조하고 있는 곳이 달라서 false이다.
> 원시 타입은 값(value)로 저장되고, 객체들은 참조(reference)로 저장된다.

# 함수
- 함수는 특별한 프로퍼티를 가진 새로운 형태의 객체이다.
```javascript
  const foo = function() {};
  foo.name; // 'foo'
  foo.length; // 1
  
  foo.bar = 'baz';
  foo.bar; // 'baz'
```
- 일반적인 객체 같이 함수에 새로운 프로퍼티를 추가하는 것도 가능하다.
- 함수는 다음과 같은 조건을 만족하기 때문에 1급 객체이다.
1. 다른 함수의 인자값으로 넘겨질 수 있다.
2. 변수나 데이터에 할당이 가능하다.
3. 객체의 리턴 값으로 리턴 가능하다.
- 이러한 특성은 자바스크립트 객체가 갖는 특성과 같다.

## 메소드
- 메소드는 함수와 같이 객체의 프로퍼티이다.
```javascript
  const foo = {};
  foo.bar = function() {
    console.log('baz');
  }
  foo.bar(); // 'baz'
```

## 생성자 함수
- 리턴 값으로 생성하는 함수를 객체 그 자체로 반환하는 함수이다.
- 같은 코드를 사용하는 여러 객체들을 생성해야 할 때 생성자 함수를 유용할게 사용할 수 있다.
- 일반 함수와 다른 점은 new라는 키워드가 붙는 것과 객체 그 자체를 리턴한다는 점이다.
> 어떤 함수든 생성자 함수가 될 수 있다.

```javascript
  const Foo = function() {};
  const bar = new foo();
  
  bar; // {}
  bar instanceof Foo; // true
  bar instanceof Object; // true
```
- 생성자 함수는 Object를 리턴하게 되고, Object에 새로운 프로퍼티들을 할당하기 위해 `this`키워드를 함수에서 사용할 수 있다.
- 생성자 함수로 생성한 각 object들에게 각각의 값을 주려고 할 때 `this`키워드를 사용해 매개변수로 값을 object들에게 넘긴다.
```javascript
  const Foo = function(name) {
    this.name = name;
  }
  
  const js = new Foo('js');
  const jjss = new Foo('jjss');
  
  console.log(js); // Foo {name: "js"}
  console.log(jjss); // Foo {name: "jjss"}
  
  console.log(js === jjss); // false
```
- new 키워드 없이 Foo()라는 함수를 실행하면 일반적인 함수처럼 동작할 것이다. 내부에 있는 this 키워드는 실행 컨텍스트와 응답을 주고 받는데 Foo()라는 함수를 전역 컨텍스트에서 실행시키게 되면 전역 컨텍스트 시점의 this인 window 객체에 this 프로퍼티가 추가 된다.

# 래퍼 오브젝트 (Wrapper Object)
- String, Number, Boolean 과 같은 원시타입을 new 키워드로 생성하면 원시 타입에 대한 래퍼 오브젝트가 생성된다.
- String은 인자로 들어온 값들을 원시 문자열로 반환하는 전역함수이다.
```javascript
  console.log(String(1234)); // '1234'
  console.log(String(true)); // 'true'
  console.log(String(null)); // 'null'
  console.log(String(undefined)); // 'undefined'
  console.log(String(1234)) === 1234; // false
  console.log(String(1234)) === '1234'; // true
```
- new 키워드를 붙이면 String은 생성자 함수로 사용이 가능하다.
```javascript
  const pet = new String('dog');
  console.log(typeof pet); // object
  console.log(pet === 'dog'); // false
  
  console.log(pet);
  /*
  String {"dog"}
    0: "d"
    1: "o"
    2: "g"
    length: 3
  */
```

# 오토박싱
- 원시 타입에 프로퍼티를 할당할 때 원시타입을 잠시 래퍼객체로 자동으로 변환해주는 과정
- 특정한 원시타입에서 프로퍼티나 메소드를 호출하려 할 때, 원시타입을 오토박싱 하고 이것을 래퍼 오브젝트에 넣는다. 그리고 프로퍼티에 접근하고 값을 이용한 뒤 지운다. 이 과정은 원시타입이나 그 변수에 전혀 영향을 미치지 않는다.
- undefined나 null과 같이 래퍼객체가 없는 원시타입에 프로퍼티를 할당하려고 하면 에러가 뜬다.
