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

