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
- ㅐ
- 둘 중 하나의 변수 값을 변경하면 두 변수 값의 모두 바뀐다
