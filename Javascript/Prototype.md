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
- 위 코드처럼 \_\_proto__를 직접
