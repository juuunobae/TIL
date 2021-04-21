### 자바스크립트에는 대표적인 2가지 문접적 카테고리가 있다.
1. Statements - 문장
2. Expressions - 표현식

- 표현식은 문장처럼 동작할 수 있기 때문에 둘을 구분하는 것은 중요하다. 그래서 표현문이 존재한다.
- 반대로 문장은 표현식처럼 동작할 수 없다.

# 표현식(Expressions)
### 표현식은 값을 만들어낸다.
- 표현식은 값 하나로 귀결되는 자바스크립트 코드 조각이다. 

```javascript
  2 + 2 * 3 / 2
  
  (Math.random() * (100 - 20) + 20
  
  functionCall()
  
  window.history ? useHistory() : noHistoryFallback()
  
  1+1, 2+2, 3+3
  
  declaredVariable
  
  true && functionCall()
  
  true && declaredVariable
```

- 위의 모든 코드는 표현식이다. 표현식은 코드 중 값이 들어가는 곳이면 어디에나 넣을 수 있다.

## 표현식은 받드시 상태를 바꿀 필요는 없다.

```javascript
  const assignedVariable = 2 // 이건 문장이다. assignedVariable은 상태이다.
  assignedVariable * 4 // 표현식이다.
  assignedVariable * 10 // 표현식이다.
  assignedVariable - 10 // 표현식이다.
  console.log(assignedVariable); // 2
```

- 위의 코드의 모든 표현식에도 불구하고 assignedVariable의 값은 여전히 2이다. 
- 섹션의 제목에 반드시란 단어를 사용한 이유는 함수호출은 표현식이기 때문이다. 하지만 함수는 값을 변화시키는 문장을 포함할 수 있다.

- foo내부의 foo()함수는 undefined나 어떤 다른 값을 반환할 수 있는 표현식이다. foo가 다음과 같이 작성되었다면

```javascript
  const foo = foo() => {
    assignedValue = 14
  }
```

-  그 땐, foo를 호출하는 것은 표현식일지라도, 함수를 호출하면 결국 상태가 바뀍게 된다. 
-  foo함수를 더 나은 방법으로 재작성하려면 문장은 다음과 같을 것이다.

```javascript
  const foo = foo() => {
    return 14; // 가독성을 위한 명시적 반환
  }
  
  assignedVariable = foo();
  
  --------------------------------------
  
  const foo = foo(n) => {
    rerurn n; 
  }
  
  assignedVariable = foo(14);
```

- 이 코드가 더욱 가독성이 좋고 어딘가에 끼워넣기 좋으며 표현식과 문장사이에서 확연히 구분이 된다

# 문장(Statements)
- 기본적으로 문장은 무언가 수행한다.
- 자바스크립트에서 문장은 값이 들어 와야 할 곳에 들어갈 수 없다. 
- 함수의 인자, 대입연산의 값, 연산자의 피연산자로 사용될 수 없다.

### 자바스크립트의 문장
1. if
2. if-else
3. while
4. do-while
5. for
6. switch
7. for-in
8. with (deprecated)
9. debugger
10. variable declaration

```javascript
  if (true) {
    9 + 9
  }
```

- 브라우저 콘솔에서 이 코드를 치면 18이 리턴될 것이다. 하지만 이 결과를 표현식 처럼 사용하거나 코드 내에 값이 들어갈 어딘가에 넣을 수 없다. 
- 반환된 값을 이용할 수 없으면 문장이 값을 반환하는 것은 아무런 의미가 없다.

## 함수 선언, 함수 표현식, 네임드함수 표현식
- 함수 선언은 문장이다.
```javascript
  function foo(func) {
    return func.name;
  }
```

- 함수 표현식은 표현식이다. 익명한수라 부르는 것들
```javascript
  console.log(foo(function() {})); // ""
```

- 네임드 함수 표현식은 표현식이다.
```javascript
  console.log(foo(function myName() {})); // 'myName'
```

#### 표현식으로서의 함수와 선언으로서의 함수의 구분
- 값이 들어올 곳에 함수를 선언할 때마다, 자바스크립트는 그것을 값으로 다루려 할 것이고, 만일 그 함수가 값으로 사용될 수 없다면 에러가 발생할 것이다.
- 반면 스크립트, 모듈, 블록 문장(값이 들어가는 곳이 아닌 위치에 있는)의 전역 단계에 함수를 선언하는 것은 결과적으로 함수선언이다.

### 예제
```javascript
  if() {
    function foo() {} // 블록의 가장 상위 레벨, 함수 선언
  }
  
  function foo() {} // 전역 레벨, 함수 선언
  
  function foo() {
    function bar() {} // 블록의 가장 상위 레벨, 함수 선언
  }
  
  function foo() {
    return function bar() {} // 네임드 함수 표현식
  }
  
  foo(function() {}) // 익명 함수 표현식
  
  fucntion foo() {
    return function bar() {
      function baz() {} // 블록의 가장 상위 레벨, 함수 선언
    }
  }
  
  function() {} // 문법 에러: 함수 문장은 이름이 필요하다.
```
  
