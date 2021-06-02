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
