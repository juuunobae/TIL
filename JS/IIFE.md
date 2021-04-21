### 자바스크립트 함수와 함께 자주 사용되는 코딩 패턴 중 하나는 Immediately-invoked Function Expression(IIFE)
> IIFE가 무엇인지 왜 필요한지 이해하기 전에 JS함수에 관한 몇가지 개념들을 짚고 넘어갈 필요가 있다.

### 자연스러운 함수 정의 
```javascript
  function sayHi() {
    alert('Hello, World');
  }
  
  sayHi();
```

1. 1-3번째 줄은 sayHi()라는 이름의 함수를 정의한다.
2. 5번째 줄에서는 `()`문법을 이용해 정의한 함수를 불러온다.

- 이 함수의 정의는 항상 function 키워드로 시작한다. 뒤에는 함수의 이름이 따라오고 이름을 생략하면 문법에 어긋난다.

### 함수 표현식
```javascript
  const = 'Hello, World';
  const sayHi = function() {
    alert(msg);
  };
  
  sayHi() // 'Hello, World'
```

1. 1번째 줄은 msg 변수를 선언하고 string 값을 할당한다.
2. 2-4번째 줄은 sayHi 변수를 선언하고 function 타입의 값을 할당한다.
3. 6번째 줄은 sayHi 함수를 호출한다.

### 네임드 함수 표현식
- 함수 표현식은 이름을 가질 수 있다. 
```javascript
  const fibo = function fibonacci() {
    // 여기서 fibbonacci() 함수를 호출할 수 있다. 
    // 이 함수 표현식이 이름을 가지고 있기 때문이다.
  }
  
  // 여기서 fibonacci()를 호출하면 실패하고, fibo()는 동작한다.
```

# IIFE
- 몇가지 문체의 방식으로 쓰여진다.
```javascript
  !function() {
    alert('Hello from IIFE');
  }(); // Hello from IIFE
```

- 이 함수는 생명을 갖자마자 바로 죽는다.
- function 키워드 앞에 `!`를 붙여주면 `!`뒤에 온게 무엇이든 표현식으로 다루게 된다.
- 생기자 마자 호출되는 함수 표현식, 어떤 문테의 방식으로 쓰여지는지 상관없이 효력을 발휘 한다.
- `!`는 작성한 함수가 상태나 정의가 되지 않게 표현식으로 만들고 함수를 즉시 실행하는 것이다.

```javascript
  void function() {
    alert('Hello from IIFE');
  }();
```

- void는 함수를 식으로 다뤄지게 강제한다. 
- IIFE에서 반환 값이 필요없을 때, 위의 모든 패턴들은 실용적이다.

## 클래식한 IIFE 스타일
```javascript
  (function() {
    alert('Hello from IIFE');
  });
```
