# 'class' 키워드가 존재하 전
- **constructor**로 'classes'를 구현한다.
- console창에 Cat 클래스를 만들고 meow 함수를 추가해본다.
```javascript
  function Cat(name){
    this.name = name
  }
  
  Cat.prototype.meow = functiop meow() {
    console.log(this.name + ' meow!');
  }
  
  let cat = new Cat('Hector')
  
  cat.meow(); // Hector meow
```
> 키워드 new를 이용하여 cat을 만들었다.

- new 키워드를 사용하지 않으면 에러는 나지않지만, 최상위 오브젝트인 window 오브젝트의 name 프로퍼티만 수정된다.
```javascript
  cat = Cat('Hector');
  
  window.name // 'Hector'
```
> this가 참조하는 방식의 문제이다.

# 프로토타입은 어디에 존재하는가
- consloe에서 프로토타입 체인을 볼 수 있다.
```
  cat = new Cat('Hector')
  
  Cat {name: 'Hector'}
    name: "Hector"
   __protp__:
    meow: ƒ meow()
    constructor: ƒ Cat(name)
    __protp__: Object
```

- cat은 name을 가지고 있는 오브젝트이다. 또, meow함수를 가지고 Cat생성자 함수를 가진 **proto**라는 오브젝트를 가지고 있다. 이 오브젝트/프로토타입은 자바스크립트 오브젝트 중에 최상위 오브젝트인 **Object**도 가지고 있다.

```
  delete cat.__proto__.meow
```
- console에 위의 코드를 입력하게 되면 모든 cat 오브젝트의 `meow()`메소드를 삭제하게 된다.
  - 모든 cat오브젝트가 같은 프로토타입에 대한 참조를 공유하기 때문이다.
- cat과 같은데 `meow()`메소드 대신 `bark()`메소드를 가진 Dog클래스를 만들어본다.
```javascript
  function Dog(name){
    this.name = name
  }
  
  Dog.prototype.bark = function bark(){
    console.log(this.name + ' ouaf!');
  }
  
  let dog = new Dog('Rex');
  
  dog.bark(); // Rex ouaf!
```
- 아래의 코드는 금지된 심각하게 나쁜 코드이다.
```
  cat.__proto__ = dog.__proto__
```
- cat안에서는 아래와 같은 일이 일어난다.
```
  cat
  
  Cat {name: 'Hector'}
    name: "Hector"
   __protp__:
    bark: ƒ bark()
    constructor: ƒ Cat(name)
    __protp__: Object
```
- 아직 Cat이지만 프로토타입은 Dog의 프로토타입을 갖게 된다.

# class 사용
### 자바스크립트 클래스는 ECMAScript 2015에서 도임된 현재 존재하는 자바스크립트의 프로토타입기반 상속을 다루는 문법적 부가기능입니다. 클래스문법은 새로운 객체지향 상속 모델을 자바스크립트에 도입하진 않습니다.
> MDN에 명시되어 있는 클래스의 정의

