# GraphQL이란
- sql과 마찬가지로 쿼리 언어이다.
- spl과 언어적 구조 차이가 매우 크고, 쓰이는 방식도 차이가 크다.
- sql은 `데이터베이스` 시스템에 저장된 데이터를 효율적으로 가져오는 것이 목적이다.
- graphQL으 `웹클라이언트`가 서버로부터 데이이틀 효율적으로 가져오는 것이 목적이다.
- sql의 문장은 주로 백앤드 시스템에서 작성하고 호출한다.
- graphQL은 주로 클라이언트 시스템에서 작성하고 호출다.
---
- 서버사이드 gql 애플리케이션은 gql로 작성된 쿼리를 입력으로 받아 쿼리를 처리한 결과를 다시 클라이언트로 돌려준다.
- HTTP API 자체가 특정 데이터베이스나 플랫폼에 종속적이지 않은 것처럼 마찬가지로 gql 역시 어떠한 특정 데이터베이스나 플랫폼에 종속적이지 않는다.

# REST API와 비교
## REST API
- 주로 URL, METHOD를 조합하여 다양한 Endpoint가 존재한다.
- 각 Endpoint마다 데이터베이스 SQL쿼리가 달라진다.

## GraphQL API
- Endpoint를 하나만 둔다. 대신 쿼리 조함으로 불러오는 데이터의 종류를 결정하게 된다.
- gql스키마의 타입마다 데이터베이스 SQL쿼리가 달라진다.

> gql API 시스템을 사용하면 REST API 시스템의 여러번 네트워크 호출을 해야 하는 상황을 단 한번의 네트워크 호출로 처리를 할 수 있다.

# GraphQL의 구조
## 쿼리 / 뮤테이션 (query / mutation)
- 쿼리와 응답내용의 구조와의 관계는 놀랄 만큼 직관적이다.
- 요청하는 쿼리문의 구조와 응답받은 데이터의 구조는 거의 일치한다.
```javascript
	{ 
    hero {
		  name
		}
	}
	
	--------------------------
	{
		'data': {
			'hero': {
				name: 'js'
			}
		}
	}
```

- 쿼리는 데이터(R)를 읽는데 사용하고, 뮤테이션은 데이터를 변조(CUD)하는데 사용한다는 개념적인 규약을 정해놓은 것이다.

```sql
	{
	  human(id: '1000') {
      name
	    heigth
	  }
	}
	
	query HeroNameAndFriends($episode: Episode) {
    hero(episode: $episode) {
      name
      friends {
        name
      }
    }
  }
```
- 
