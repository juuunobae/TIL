# Restful
- 클라이언트와 서버가 통신하기 위한 정해놓은 규약의 형태
- rest API 메시지를 읽는 것 만으로도 메시지가 의도하는 바를 명확하게 파악할 수 있다.
- 기본적으로 http를 사용하여 요청 및 응답을 처리
  - http 인프라를 그대로 사용하기 때문에 Rest API 사용을 위한 별도의 인프라 구축이 필요없다.
- 클라이언트가 리소스를 요청하면 서버는 해당 리소스를 응답해주기만 하면 된다.
  - 클라이언트와 서버가 독립적으로 운영 가능

## Restful API란
- 분산 시스템 설계를 위한 이키텍쳐 스타일
  - 아키텍쳐 = 구성
- 사이트 구성 원리
  - 사이트를 어떻게 구성해야하는가 원리 
  
### Rest
  - 사이트 구성원리
### Restful
  - Rest한
### Restful API
  - Rest한 API
> 사이트 구성 원리를 준수하는 API

### REpresentational
  - 표현
### State
  - 상태
### Transfer
  - 전송
  
- `자원`의 `표현`을 가지고 `상태`를 전달한다.

### 구현 방법

- 자원을 uri로 명시해준다.
  - 모든 URI는 자원으로 나타낸다.
  ```
    GET /sports/soccer/show
    GET /sports/soccer/players/11/delete
  ```
  > URI에는 동사가 들어가면 안 된다.
  ```
    GET /sports/soccer
    DELETE /sports/soccer/players/11
  ```
  
- 상태를 http 메서드로 해준다.
  - 모든 동장은 Method로 나타낸다.
  ```
    GET 조회 
    POST 생성
    PUT 수정
    DELETE 삭제
  ```
  > PUT = 모든 데이터를 수정할 때 
  > PATCH = 데이터의 일부를 수정할 때
  
- 표현은 header로 전달 할 수 있다.
  - 클라이언트가 전달 받고자하는 데이터를 명시
  - 리소스의 응답 타입은 header로 나타낸다.
  ```
    Content-Type = 클라이언트가 요청하는 데이터 타입
  ```
  - 응답받고 싶은 타입은 Accept를 사용하면 된다.
  ```
    Accept: image/jpg
    
    무엇을 적어야 할 지 모르겠다면 그냥 브라우저가 알아서 설정해서 보내는 accept를 사용하면 된다.
  ```

 


