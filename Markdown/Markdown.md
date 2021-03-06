# 마크다운

## 1. 마크다운이란
2004년 존과 애론에 의해 개발된 plain-text 포맷을 기본으로한 경량형 마크업 언어이다.
.md 확장자파일로 텍스트 에디터에서도 키보드하나로 쉽게 포맷하면서 빠르게 문서를 작성할 수 있다.
또 Pull Request 설명을 작성할 때도 쓰이고 많은 디지털 노트를 사용할 때에도 간편하게 키보드로 작성할 수 있게 도와준다.
문법이 간결하고 별도의 도구 없이도 작성이 가능하다.
    
## 2. 마크다운 문법

### 2.1 제목(Header)
html의 **h1** 태그부터 **h6** 태그까지 표현할 수 있다.
- header 1
```
# header1
```
✅결과
# header1 
    
- header 2
```
## header2
```
✅결과
## header2

- h1과 h2는 =과 -로도 표현할 수 있다.
```
header1
===

header2
---

기호를 2개 이상 사용하면 대체가 가능하다.
```

- header 3, 4, 5, 6
```
### header3
#### header4
##### header5
###### header6
```
✅결과
### header3
#### header4
##### header5
###### header6
-----

### 2.2 목록
순서가 없는 목록, 순서를 표기하는 목록 두 가지를 표현할 수 있다.
- 순서가 없는 목록
    - **-**, __*__, __+__ 를 사용하여 작성한다.
```
- 목록
* 목록
+ 목록

- 목록
    - 목록
```
✅결과
- 목록
* 목록
+ 목록 

- 목록
    - 목록
---
- 순서가 있는 목록
    - 숫자를 사용하여 작성한다.
```
1. 목록
2. 목록
3. 목록
```
✅결과
1. 목록
2. 목록
3. 목록
---

### 2.3 강조
- 굵게, 이텔릭체, 취소선을 표현할 수 있다.
```
*이텔릭체*
_이텔릭체_

**굵게**
__굵게__

~취소선~
```
✅결과<br/>
*이텔릭체*<br/>
**굵게**<br/>
~취소선~<br/>

---

### 2.4 링크(Links)
- 일반 URL이나 <>안의 URL은 자동으로 Link로 바뀐다.
```
깃허브: https://github.com
google: <https://google.com>

[깃허브](https://github.com)
```
✅결과  
깃허브: https://github.com  
google: <https://google.com>
  
[깃허브](https://github.com)

---

### 2.5 인용문
- '>'를 사용하고 중첩해서 사용할 수 있다.
```
>인용문
>>중첩된 인용문
>>>중중첩된 인용문

> - 인용문 안에 다른 마크다운 요소
```
✅결과
>인용문  
>>중첩된 인용문  
>>>중중첩된 인용문
  
> - 인용문 안에 다른 마크다운요소

---

### 2.6 코드

#### 인라인 블럭
- '\`'로 코드를 묶어준다.  
<pre>
`const a = 'hello'`
</pre>
✅결과  
`const a = 'hello'`  

#### 코드 블럭
- '\`\`\`' 로 코드를 묶어준다.
<pre>
``` 
const a = 'hello';
console.log(a);
```
</pre>
✅결과  
```
const a = 'hello';
console.log(a);
```


- '\`\`\`'뒤에 언어 종류를 적어주면 그 언어에 맞게 코드를 표현해준다.  
<pre>
```javascript
const a = 'hello';
console.log(a);
```

```python
a = 'hello'
print(a)
```
</pre>
✅결과
```javascript
const a = 'hello';
console.log(a);
```
```python
a = 'hello'
print(a)


```
---

### 2.7 표
- |(pipe)로 행을 나누고 \-(hyphen)으로 헤더를 구분한다.
- 헤더를 구분하는 열의 각 행에 :(colon)을 사용해 text 정렬을 할 수 있다.
```
| 언어 | 만든연도 | 프레임워크|
|:----|:------:|-------:|
| javascript | 1995 | react |
| python | 1991 | django |
| java | 1995 | spring |
```
✅결과
| 언어 | 만든연도 | 프레임워크|
|:----|:------:|-------:|
| javascript | 1995 | react |
| python | 1991 | django |
| java | 1995 | spring |

---

### 2.8 체크박스
- \-, \*, \+ 뒤에 사이가 한 칸 띄워진 대괄호를 작성하면 빈 체크박스, 사이에 x가 적힌 대괄호를 작성하면 체크가 된 체크박스가 생성된다.
```
- [ ] html
- [x] javascript
```
✅결과
- [ ] html
- [x] javascript

---

### 2.9 이미지
- ![이미지 이름](이미지 URL) 순으로 적어주면 된다.
- 이미지의 크기를 조절할 때는 html문법으로 작성해야 하며 width값과 height값을 넣어주면 된다.
- 이미지에 링크를 걸려면 [![!이미지 이름](이미지 URL)](연결 하고자 하는 링크 URL "마우스 오버 시 나타낼 링크 title)
```
![react img](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/220px-React-icon.svg.png)
<img src='https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/220px-React-icon.svg.png' width='100px' height='100px' />
[![react img](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/220px-React-icon.svg.png)](https://en.wikipedia.org/wiki/React_(web_framework) 'react wiki')
```
✅결과  
![react img](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/220px-React-icon.svg.png)  
<img src='https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/220px-React-icon.svg.png' width='100px' height='100px' />  
[![react img](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/220px-React-icon.svg.png)](https://en.wikipedia.org/wiki/React_(web_framework) 'react wiki')

---
