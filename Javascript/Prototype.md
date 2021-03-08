### 자바스크립트 객체에는 [[Prototype]]이라는 내부 프로퍼티(프로토타입 링크)가 있고, `다른 객체를 참조하는 레퍼런스로 사용`한다.
### 객체에서 프로퍼티를 탐색할 때 객체 내에 프로퍼티가 존재하지 않으면 undefined를 출력하고 끝나는게 아니라 [[Prototype]]참조를 따라가면서 프로퍼티가 존재하는지 탐색한다. `(프로토타입 연쇄)`     

# 프로토타입 객체(.prototype)와 프로토타입 링크(.\_\_proto__)
- 리터럴 형식으로 생성한 객체들은 자바스크립트 엔진 입장에서 생성함수로 생성한 것과 똑같이 해석된다.
```javascript
   const obj = { a: 1, b: 2 };
   // 리터럴로 생성한 obj는 실제로 아래와 같다.
   const obj = new Object({ a: 1, b: 2 })
```
- 크롬 기준으로 자바스크립트의 객체에는 \_\_proto__ 라는 프로퍼티가 존재하고 함수에는 prototype이라는 프로퍼티가 존재하는데
- `객체의 __proto__를 프로토타입 링크, 함수의 prototype을 프로토타입 객체라고 할 수 있다.`
- 객체 생성 시 생성된 객체의 프로토타입 링크가 생성 함수의 프로토타입 객체를 참조하는 형태를 하게 된다.

> `즉 obj객체가 생성되면 프로토타입 링크(__proto__)가 객체의 생성 함수의 prototype이 가르키는 객체를 참조하게 되는 것이다.`

```javascript
   const obj1 = { a: 1, b: 2 };
   const obj2 = new Object({ c: 3, d: 4 });
   
   console.log(obj1.__proto__ === Object.prototype); // true
   console.log(obj2.__proto__ === Object.prototype); // true
   console.log(obj1.__proto__ === obj2.__proto__); // true
   
   console.log(obj1.__proto__.valueOf === Object.prototype.valueOf); //true
   console.log(obj2.__proto__.vlaueOf === Object.prototype.valueOf); //true
   console.log(obj1.valueOf === Object.prototype.valueOf); //true
   console.log(obj2.valueOf === Object.prototype.valueOf); //true
```
- 위 코드는 obj1과 obj2가 프로토타입 링크에 의해 동일한 프로토타입 객체(Object.prototype)를 참조하고 있음을 나타내고 있다.

```javascript
   const a = 0[1, 2, 3];
   const b = new Array([4, 5, 6]);
   
   console.log(a.__proto__ === Array.prototype); //true
   console.log(b.__proto__ === Array.prototype); //true
   console.log(a.forEach === b.__proto__.forEach && b.__proto__.forEach === Array.prototype.forEach); //true
```
```javascript
   const a = 'javascript';
   
   console.log(a.replace === String.prototype.replace); //true
```
- 다른 자료형 역시 동일하다. 
- number, string, boolean 같은 원시 자료형들은 auto boxing(값을 객체 타입으로 변환)이 일어난다.

```javascript
   function Person(name){
      this.name = name;
   }
   
   Person.prototype.sayName = function() {
      console.log('my name is ' + this.name);
   };
   
   const p1 new Person('man');
   console.log(p1); // { name: 'man' }
   p1.sayName(); // my name is man
```
- 직접 정의한 함수가 프로토타입 객체가 있고, new 키워드를 사용해서 객체를 생성하면 동일한 현상이 발생한다.

# 포로토타입 연쇄
- 객체에서 프로퍼티를 호출하면 프로토타입 연쇄에 의해 아래와 같은 과정이 일어난다.
1. 객체 내에 해당 프로퍼티를 찾는다.
2. 객체 내에 프로퍼티가 존재하지 않으면 객체가 참조(\_\_proto__)하고 있는 prototype객체에서 프로퍼티를 찾는다.
3. 최상위 prototype까지 탐색하며 2번항목을 반복한다. (\_\_proto__.\_\_proto__.\_\_proto__...)
4. 존재하지 않으면 undefined를 반환한다.

- 이렇게 상위 prototype 참조를 타고 올라가는 과정을 prototype 연쇄라고 하며, 자바스크립트 명세에서는 [[prototype]]이라고 표현한다고 한다.

```javascript
   function Test(){
      this.a = 10;
   }
   
   Test.prototype.b = 20;
   Object.prototype.c = 30;
   
   const obj new Test();
   
   console.log(obj); // Test { a: 10 }
   console.log(obj.a); // 10
   console.log(obj.b); // 20
   console.log(obj.c); // 30
   console.log(obj.d); // undefined
```
- 위 코드처럼 \_\_proto__를 직접 명시하지 않아도 프로토타입 연쇄가 발행한다.
- obj를 콘솔에 찍어보면 new 바인딩에 의해서 객체 obj에 a라는 프로퍼티가 등록되어있음을 확인할 수 있다.
- b, c라는 프로퍼티는 객체 obj에 존재하지 않음에도 호출됨을 볼 수 있다.
   - 프로토타입 연쇄 과정을 통해 프로퍼티를 찾아냈기 때문이다.

```javascript
   function Test(){
      this.a = 10;
   }
   
   Test.prototype.b = 20;
   Object.prototype.c = 30;
   
   const obj new Test();
   
   // obj.__proto__ === Test.prototype -> true
   console.log(obj.__proto__.b); // 20
   // obj.__proto__.__proto__ === Object.prototype -> true
   console.log(obj.__proto__.__proto__.c); // 30
```
- obj의 [[prototype]] 링크(\_\_proto__)가 Test 함수의 prototype과 같고, 이를 통해 b를 참조할 수 있다.
- obj의 [[prototype]] 링크(\_\_proto__)의 [[prototype]] 링크가 Object 함수의 prototype과 같고, 이를 통해 c를 참조할 수 있다.

# 프로토타입 체인
- 프로토타입 체인을 연결하면 메모리 관점에서 장점이 있다.

```javascript
   function Person(name){
      this.sayName = function() {
         console.log(`안녕하세요 ${this.name}입니다.`);
      };
   }
   
   let p1 = new Person('js');
   let p2 = new Person('jjss');
   
   console.log(p1); // Person { name: 'js', sayName: [Function] }
   p1.sayName(); // 안녕하세요 js입니다.
   console.log(p2); // Person { name: 'jjss', sayName: [Function] }
   p2.sayName(); // 안녕하세요 jjss입니다.
   
   console.log(p1.sayName === p2.sayName); //false
```
- 위 코드에서 클래스의 역할을 하는 Person 함수는 멤버변수 name과, name을 출력하는 sayName이라는 메소드를 정의하는 행위를 한다.
- new Person으로 생성된 객체 p1, p2는 각각 name과 sayName 함수를 가지고 있는 모습을 볼 수 있다.
- sayName이라는 메소드가 공통적으로 사용됨을 볼 수 있다.
- 이를 prototype을 사용할 수 있도록 바꿔줄 수 있다.

```javascript
   function Person(name) {
      this.name = name
   }
   
   Person.prototype.sayName = function() {
      console.log(`안녕하세요 ${this.name}입니다.`);
   };
   
   let p1 = new Person('js');
   let p2 = new Person('jjss');
   
   console.log(p1); // Person { name: 'js' }
   p1.sayName(); // 안녕하세요 js입니다.
   console.log(p2); // Person { name: 'jjss' }
   p2.sayName(); // 안녕핳세요 jjss입니다.
   
   console.log(p1.sayName === p2.sayName); //true
```

- 공통 메소드인 sayName을 Person 함수의 prototype에 정의한다.
- p1과 p2에서 sayName이 호출되고 있지만 각 객체안에는 sayName 프로퍼티가 보이지 않고, 하단 console.log를 보면 true를 나타내고 있다.
   - 프로토타입 체인으로 p1과 p2의 \_\_proto__는 같은 prototype, 즉 Person의 prototype을 참조하고 있기 때문이다.
   - 각 객체에 sayName 함수를 할당하는 것 보다 prototype에 정의된 sayName함수를 참조하는 것이 메모리 측면에서 이득이다.

```javascript
   Array.prototype.findOneIndex = function(value) {
      for (let i = 0, length = this.length; i < length; i++) {
         if (this[i] === value) {
            return i;
         }
      }
   }
   
   console.log([5, 4, 3, 2, 1].findOneIndex(4)); // 1
   
   Number.prototype.toDollor = function() {
      return this.valueOf() + '$';
   };
   
   let salary = 100;
   console.log(salary.toDollor()); // 100$
```

- 위 코드처럼 Number, String, Array, Object 같은 네이테브 함수의 prototype에 나만의 공통 함수를 정의하여 사용할 수 있다.
   - 다른 사람들과 일하다보면 prototype에 뭘 붙여놓는 것은 골치아픈 일이 될 수 있다.
   - 필요하다면 개인적으로 모듈을 만들어서 사용하는 것을 권장한다.

# prototype 상속 패턴 구현
- prototype에 공용 메소드를 정의하고, 생성된 객체가 눈에 보이지 않는 메소드를 참조하는 모습은 다른 언어의 class를 상속하여 사용하는 모습과 비슷한 느낌을 준다.

```javascript
   function Parent(name) {
      this.name = name
   }
   
   Parent.prototype.sayName = function() {
      console.log(`my name is ${this.name}`);
   }
   
   function Children(name, age) {
      Parent.call(this, name);
      this.age = age;
   }
   
   Children.prototype = Object.create(Parent.prototype); 
   // Parent.protoype을 [[prototype]]으로 갖는 객체를 Children.prototype에 연결
   
   Children.prototype.sayAge = function() {
      console.log(`my age is ${this.age}`);
   };
   
   let p1 = new Children('js', 20);
   console.log(p1); // { name: 'js', age: 20 }
   p1.sayName(); // my name is js
   p1.sayAge(); // my age is 20
```
- prototype을 조작하여 만든 상속 패턴이다.
- Children 함수 내에서 this를 Parent 함수에 넘겨서 호출하는 것으로 부모의 생성자를 호출하는 부분을 구현한다.
- Children의 prototype을 Parent의 Prototype과 관계 맺어줌으로써 상속 형태를 구현 했다.  

> prototype을 사용하여 상속을 구현하면 java의 상속과 크게 다른점이 생기는데
> java에서는 상속된 클래스의 객체를 생성할 경우, 각 객체(인스턴스)마다 부모 영역이 메모리 공간에 잡힌다고 한다.
### java
#### p1 객체
| | |
|---|---|
| Parent | |
| sayName | |
| Children | |
| sayAge | |

#### p2 객체
| | |
|---|---|
| Parent | |
| sayName | |
| Children | |
| sayAge | |

- java의 p객체들은 모두 Parent 영역까지 가지고 있는 모습이다.

### javascript
#### Parent.prototype 객체
| | |
|---|---|
| [[prototype]] | |
| sayName | |

#### Children.prototype 객체
| | |
|---|---|
| [[prototype]] | Parent.prototype 객체 참조 |
| sayName | |

#### p1 객체
| | |
|---|---|
| [[prototype]] | Children.prototype 객체 참조 |
| ... | |

#### p2 객체
| | |
|---|---|
| [[prototype]] | Children.prototype 객체 참조 |
| ... | |

- javascript의 p객체들은 [[prototype]]을 통해서 하나의 Parent를 참조하고 있는 모습이다.
- 상속관계가 깊어질수록 [[prototype]] 과정이 많이 일어나야 하기 때문에 참조에 대한 이슈가 있을 수 있다.

# javascript에서는 객체간 관계를 `작동 위임`이라는 디자인 방식으로 구현할 수 있다.
- `작동 위임` 방식은 객체의 [[prototype]]이 되는 객체를 직접 지정하는 방식이다.
- Object.create(prototypeObj) 혹은 Object.setPrototypeOf(obj, prototypeObj) 메소드를 사용하여 쉽게 prototype 관계를 지정해줄 수 있다.
   - Object.create는 인자로 받은 객체를 [[prototype]]으로 사용하는 빈 객체{}를 생성해준다.
   - Object.setPrototypeOf는 첫번 째 인자의 [[prototype]]을 두번 째 인자에 연결해준다.
```javascript
   let Person = {
      sayName: function() {
         console.log(`my name is ${this.name};
      };
   };
   
   let p1 = Object.create(Person);
   p1.name = 'js';
   p1.sayName(); // js
   console.log(p1.__proto__ === Person); // true
   
   let p2 = { name: 'jjss' };
   Object.setPrototypeOf(p2, Person);
   p2.sayName(); // jjss
   console.log(p2.__proto__ === Person); // true
```
- 클래스 역할을 하는 function도 없고, prototype을 조작할 일도 없다.
- 클래스 패턴에서는 기능을 정의한 class를 만들고 -> class간 관계를 만들고 -> 객체를 생성했지만, 
- 작동 위임에서는 기능을 정의한 객체를 만들고 -> 객체를 이어줌으로써 동일한 동작을 구현할 수 있다.

#### Person 객체
| | |
|---|---|
| [[prototype]] | |
| sayName | |


#### p1 객체
| | |
|---|---|
| [[prototype]] | Person 객체 참조 |
| name | |

#### p2 객체
| | |
|---|---|
| [[prototype]] | Person 객체 참조 |
| name | |

- prototype과의 관계가 빠지면서 깔끔해진다.

```javascript
   let parent = {
      sayName: function() {
         console.log(`my name is ${this.name}`);
      },
   };
   
   let children = {
      sayAge: function(){
         console.log(`my age is ${this.age}`);
      },
   }
   
   Object.setPrototypeOf(children, parent);
   
   function makePerson(name, age) {
      let p = {
         name: name,
         age: age
      }
      
      Ogject.setPrototypeOf(p, children);
      return p;
   };
   
   let p1 = makePerson('js', 20);
   p1.sayName(); // my name is js
   p1.sayAge(); // my age is 20
```
