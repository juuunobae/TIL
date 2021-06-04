# 4가지 규칙
### `new` 연산자를 사용할 때는 다음과 같은 4가지 일이 벌어진다.
1. 새로운 빈 오브젝트 생성
2. `this`를 새롭게 생성된 오브젝트에 바인드
3. 새롭게 생성된 오브젝트의 프로퍼티에 `proto`라고 하는 생성자 함수의 프로토타입 오브젝트 추가
4. 함수에서 완성된 오브젝트가 반환될 수 있도록, `return this`를 함수의 마지막 부분에 추가

# 예제
#### 생성자 함수 `Student`를 만들어 2개의 파라미터 `name`, `age`를 갖고, 이 프로퍼티를 `this`의 값에 세팅한다.
```javascript
  function Student(name, age) {
    this.name = name;
    this.age = age;
  }
```
#### 생성자 함수를 `new` 연산자로 호출하고, 인자를 전달한다.
```javascript
  var first = new Student('jun', 28);
```
- 위 코드를 실행시키면
1. 새로운 오브젝트 `first`가 만들어졌다.
2. `this`가 `first` 오브젝트에 바운드 되고, `this`를 참조하면 `first` 오브젝트가 참조된다.
3. **proto**가 추가되고, `first.__proto__`는 `Student.Prototype`을 가리킨다.
4. 새로운 `first`오브젝트가 리턴되어 `first`변수에 할당된다.

```javascript
  console.log(first.naem); // jun
  console.log(first.age); // 28
```

# 프로토타입(Prototypes)
### 모든 자바스크립트 오브젝트는 오브젝트는 프로토타입을 가지고 있다. 모든 오브젝트는 프로토타입에서 메소드를 상속받고 프로퍼티를 상속 받는다.
- 개발자 도구 콘솔을 열고 함수를 타이핑 하면
```javascript
  function Student(name, age) {
    this.name = name;
    this.age = age;
  }
```
```
  Student.prototype;
  // Object {...}
```
- 오브젝트가 반환된다.
- 새로운 Student를 만들어 보면
```javascript
  var second = new Student('jeff', 50);
```

```
  Student.prototype.constructor;
  // function Student(name, age) {
  //   this.name = name;
  //   this.age = age;
  //  }
```
- `Student.prototype.constructor`가 `Student` 생성자 함수를 가리키고 있음을 알게 된다.
<img width="421" alt="스크린샷 2021-06-04 오후 1 09 58" src="https://user-images.githubusercontent.com/42345122/120744549-30a5a500-c536-11eb-8434-50ae40c791fa.png">
- 생성자 함수는 `.prototype`이라 불르니느 프로퍼티를 가진다. 이 프로토타입은 프로퍼티로 `.constructor`라 불리는 오브젝트를 가지고 이 오브젝트는 생성자 함수를 다시 가리킨다.
- `new` 연산자를 이용하여 새로운 오브젝트를 만들 때, 각각의 오브젝트는 `.__proto__` 프로퍼티를 갖는다.
- `.__proto__`프로퍼티는 새로운 오브젝트를 다시 `.prototype`으로 연결해준다.

> 이것들은 상속 때문에 중요하다. 프로토타입 오브젝트는 그 생성자 함수로 만들어진 모든 오브젝트에서 공유된다. 함수나 프로포티를 포로토타입에 추가하면 모든 오브젝트가 그것들을 이용할 수 있다는 말이다.
