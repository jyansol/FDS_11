# Fetch API
- XML : JSON이 없던 때의 통신기술
- `polyfill` : babel (기능은 빼고 문법만 구버전으로 바꿔줌), polyfill은 최신 브라우저기능과 똑같이 만들어진 라이브러리
  * Array.prototype.includes (ES2015) =>  Array.prototype.includes polyfill => npm install
  * fetch를 쓰고싶다 => fetch polyfill 을 포함시켜야함 `깃헙에서 만듬`
- fetch를 사용하면 promise가 자동으로 생성됨
    * axios보다는 불편함이 있음
    * axios는 편의 기능이 많음 일반 개발자가 만듬, 내부적으로 XMLHttpRequest를 사용하고 있는데 Service Worker 등의 최신 기술이 XMLHttpRequest를 지원하지 않으므로, Service Worker를 사용할 예정에 있는 프로젝트에서는 Axios 대신 Fetch API를 사용해야만 함 . `fetch랑만 연동해서 쓸 수 있는 최신 기술을 사용할 수 없음`
- fetch는 headers를 받고, body를 받음 (promise가 2번)

---

# Cache
- 임시저장소, 접근 속도 개선을 위해서
- 실행시킬 필요가 있다. => cache에 올림 => CPU 실행
### HTTP Cache
- status 304 => 브라우저 캐시에 저장되어있는 문서를 불러옴
### Cache의 동작방법
- 똑같은 자원을 요구했을때, 기존의 자원을 사용
- 원본과 사본이 달라지는 경우가 생김 => 어떻게 처리할 것인가 ? => 브라우저에게 유효기간 설정, 방법 설정이 가능함
  * `₩Expiration (만료)` :
정해진 시간이 지나면 캐시가 자동으로 삭제되도록 설정
  * `Validation (검증)` : 
서버에 요청을 보내서 캐시를 계속 사용할 수 있는지 확인
### Cache 관련 헤더
- Cache-Control
- ETag : (응답) 자원의 식별자를 만듬. 1번(식별자) 자료 => 브라우저에게 보낼때, 식별자를 포함시켜 전송 => 브라우저는 1번+자원 => 식별자만 비교해서 바꼈는지, 안바꼈는지 확인 가능 => 전체자원을 보내지 않아도 바꼈는지 안바꼈는지 알 수 있음 
  * 식별자로 주로 자원의 해시값이 사용되나, 마지막으로 수정된 시각, 혹은 버전 넘버를 사용하기도 함
  * `해시값`
    01. 같은 입력을 주면 항상 같은 출력이 나온다.
    01. 입력이 조금이라도 달라지면 완전히 다른 출력이 나온다.
- If-None-Match : (요청) 
  * `자원이 바뀌지 않은 경우` : 브라우저가 요청을 보내면 Etag응답을 보냄. 다음에 요청을 보낼때 if-None-Match:Etag (같니)를 포함시켜서 보냄. 응답으로 304 Not Modified (변한게없단다)라고 보냄. body에 자원을 포함시키지 않음
  * `자원이 바뀐 경우` : 브라우저가 요청을 보내면 Etag응답을 보냄. 다음에 요청 보낼때 if-None-Match:Etag 라고 보냄. 200 OK + 바뀐 자원을 포함시켜서 보냄
> ntlify에 Etag / If-None-Match 기능이 포함되어있음
- Last-Modified
- If-Modified-Since

# CDN
- 자료를 제공하기 위한 네트워크
  * 서버를 국가별, 지역별 등에 뿌려두고 가까운 서버를 사용해서 자원을 받을 수 있게
  * CDN이 적용되어있나요?

# REST API
- GET/todos, POST/todos 등과 같은 식의 통신. 서버와 클라이언트간에 통신을 하고싶은 경우
  * 단점 
    01. 각각의 자원마다 경로가 따로 있음. 여러 자원이 동시에 필요한 경우 요청을 여러 번 보내야함
    01. 일부 속성의 필요하더라도 전체 속성을 가져와야만 함
# GraphQL
- 2015년 페이스북에서 공개함
- REST API를 대체하기 위해 만들어짐
- 별도의 언어
- 필요한 자원만 가지고 올 수 있음    
> https://www.apollographql.com/