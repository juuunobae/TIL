### 값에 의한 전달이 일어나는 5가지의 데이터  타입(String, Number, Boolean, Undefined, Null)을 가지고 있고 이를 원시타입이라고 부른다.
### 참조에 의한 전달이 일어나는 3갸지 데이터 타입(Object, Function, Array)를 가지고 있고 이를 객체라고 할 수 있다.

# 원시타입
- 어떠한 원시타입이 변수에 할당된다면, 그 변수를 원시타입을 가진 변수라고 생각할 것이다.
```javascript
  let x = 10;
  let y = 'abc';
  let z = null;
```
- x는 10이란 값을 가지고 있고, y는 abc란 값을 가지고 있는데 메모리상에 존재하는 이 변수들을 다음과 같이 나타낼 수 있다.

|Variables|Values|
|---|---|
|x|10|
|y|'abc'|
|z|null|

- 이런 변수들을 다른 변수에 = 키워드를 이용하여 할당할 때 새로운 변수에 값을 복사하게 되는데 이 변수들은 값에 의해 복사된다.
```javascript
  let x = 10;
  let y = 'abc';
  
  let a = x;
  let b = y;
  
  console.log(x, y, a, b); // (10, 'abc', 10, 'abc')
```
- a와 x는 둘 다 10이란 값을 갖고 있고 b와 y는 둘 다 'abc'라는 같은 값을 갖고 있지만 이들은 분리 되어있다. 값이 복사되었기 때문이다.

|Variables|Values|
|---|---|
|x|10|
|y|'abc'|
|a|10|
|b|'abc'|

- 복사하여 서로 같은 값을 가진 변수 하나의 값을 바꾸더라도 다른 변수에는 영향이 없다.
- 각각의 변수들이 아무런 관계가 없다고 생각하면 된다.

# 객체
- 원시 타입이 아닌 값이 할당된 변수들은 그 값 자체가 아닌 그 값으로 향하는 참조를 갖게 된다.
- 참조는 메모리에서 객체의 위치를 가리키고 있다. 변수는 실제로 값을 가지고 있는 것이 아니다.
- 객체는 메모리 어딘가에 생성되고, `arr = []`를 작성했을 때 변수 arr이 갖는 것은 메모리 내부에 생성된 배열이 위치하 주소이다.
```javascript
  //1
  let arr = [];
  //2
  arr.push(1);
```
- 메모리상에 존재하는 

1.
|Variables|Values|Addresses|Objects|
|---|---|---|---|
|arr|<#001>|#001|[]|

2. 
|Variables|Values|Addresses|Objects|
|---|---|---|---|
|arr|<#001>|#001|[1]|

- 위 그림을 보면 address가 원시타입과 같이 값에 의한 전달을 하는 새로운 종류의 데이터 타입이라고 가정하고, address는 참조에 의한 전달을 하는 위치를 가리키게 된다.
- arr이 가진 변수의 값(주소)는 정적이다. 변수의 값이 바뀌는 것이아니라 참조하고 있는 메모리 속 주소의 배열 값만 바뀌는 것이다.

## 참조로 할당하기
- 객체와 같은 참조 타입의 값이 `=`과 같은 키워드를 이용하여 다른 변수로 복사될 때, 그 값의 주소가 복사된다.
```javscript
  let reference = [1];
  let refCopy = reference;
```
- 위의 코드는 메모리상에서 아래와 같다

|Variables|Values|Addresses|Objects|
|---|---|---|---|
|reference|<#001>|#001|[1]|
|refCopy|<#001>|

- 각각의 변수는 같은 주소(메모리상에 실제 데이터가 저장되어 있는 곳)로 향하는 참조값을 갖는다
- 둘 중 하나의 변수 값을 변경하면 두 변수 값의 모두 바뀐다.
```javascript
  reference.push(2);
  console.log(reference, refCopy); // [1, 2] [1, 2]
```
- `reference`의 값만 변경했지만 `refCopy`의 값도 같이 바꼈다.

## 참조 재할당하기
- 참조 값을 재할당 하는 것은 오래된 참조를 대체한다.
```javascript
  let obj = { first: 'refernce' };
```
- 메모리상태

|Variables|Values|Addresses|Objects|
|---|---|---|---|
|obj|<#234>|#234|{ first: 'reference' }|

- 만약 재할당 코드를 입력하면
```javascript
  let obj = { first: 'reference' };
  obj = { second: 'ref2' };
```
- obj에 저장되었던 주소 값이 변경된다. 첫 번째 객체는 메모리상에 아래와 같이 표기가 되기는 한다.

||Variables|Values|Addresses|Objects|
|---|---|---|---|
|obj|<#678>|#234|{ first: 'reference' }|
|||#678|{ second: 'refd2' }|

- 남아있는 객체를 가리키는 참조가 남아있지 않을 때 자바스크립트 엔진은 가비지 컬렉션을 동작시킬 수 있다. 
- 프로그래머가 모든 참조를 날리고 객체를 더이상 사용할 수 없게 된 뒤 자바스크립트 엔진은 사용되지 못하는 객체를 메모리부터 안전하게 지워버리며 가비지 컬렉션이 된다.

## == and ===
- 동등함을 비교하는 연산자 둘은 참조 타입의 변수를 비교할 때 사용된다. 
- 변수가 같은 값에 대한 참조를 갖고 있다면 결과는 true가 나올 것이다.
```javascript
  let arrRef = ['Hi!'];
  let arrRef2 = arrRef;
  
  console.log(arrRef === arrRef2); // true
```

## 함수를 통한 파라미터 전달
- 원시 값들을 함수로 전달할 때, 함수는 값들을 복사하여 파라미터로 전달한다. 이것은 `=`연산자를 이용하는 것과 같다.
```javascript
  let hundred = 100;
  let two = 2;
  
  function multiply(x, y) {
    // PAUSE
    return x * y;
  }
  
  let twoHundred = multiply(hundred, two);
```
- 위의 코드 중 PAUSE 상태에서 메모리가 구성되는 원리

|Variables|Values|Addresses|Objects|
|---|---|---|---|
|hundred|100|#333|function(x, y)...|
|two|2|||
|multiply|<#333>|||
|x|100|||
|y|2|||

## 순수 함수
- 함수 중에 함수 바깥 스코프에 아무런 영향도 미치지 않는 함수를 우리는 순수 함수라고 한다.
- 함수가 원시 값들만을 파라미터로 이용하고 주변 스코프에서 어떠한 함수도 이용하지 않다면 순수함수가 된다.
- 함수안에서 만들어진 변수들은 return문이 실행되는 즉시 가비지 컬렉션 처리가 된다.
<br><br>
- 객체를 받는 함수는 주변 스코프들의 상태를 변화시킬 수 있다. 함수가 주변 스코프에 존재하는 객체를 파라미터로 받고 함수내에서 파라미터로 받은 객체를 변경하면 그 객체를 참조하고 있는 모든 변수들이 같이 변경된다.
- 비순수함수
```javascript
  function changedAgeImpure(person) {
    person.age = 25;
    return person
  }
  
  let alex = {
    name: 'Alex',
    age: 30,
  }
  
  let changedAlex = changeAgeImpure(alex);
  
  console.log(alex); // { name: 'Alex', age: 25 }
  console.log(changeAlex); // { name: 'Alex', age: 25 }
```
- 순수 함수
```javascript
  function changedAgePure(person) {
    let newPerson = JSON.parse(JSON.stringify(person));
    newPerson.age = 25;
    return newPerson;
  }
  
  let alex = {
    name: 'Alex',
    age: 30,
  }
  
  let changedAlex = changeAgePuer(alex);
  
  console.log(alex); // { name: 'Alex', age: 30 }
  console.log(changedAlex); // {name: 'Alex', age: 25 }
```
- 객체를 문자열로 변환한 후(JSON.stringify(person)) 다시 객체로(JSON.perser(JSON.stringify(person)) 변환되는 과정을 거쳐 새로운 객체를 만들고 그 결과를 새로운 변수에 할당한다. 원본 객체와 새로 생성한 객체는 같은 값을 가지지만 참조하고 있는 주소값은 다르다.
- 새로운 객체는 반환이 되어아햐고 변수에 저장되어야 한다. 그렇지 않으면 가비지 컬렉션 될 것이다. 
