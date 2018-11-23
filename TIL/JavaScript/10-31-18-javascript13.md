# JavaScript
> ## 클래스
- 생성자 : 함수를 재사용하기 위해
- 클래스 : 객체를 찍어내고, 공통의 기능을 모아두기 위함. 생성자 문법을 더 쓰기 편하고, 단점을 없앰.
- 클래스 vs 클래스 필드 : 속성 넣어주는 방법 
  * 클래스 : 생성자 constructor 만들어서
  * 클래스 필드 문법
``` 
클래스필드는 아직 정식문법이 아니다!  
```
- 클래스 상속
  * 클래스에 속성들을 만들고, 상속받기가 가능 `100% 상속!`
  ```js
  class Parent {
  // ...
  }

  class Child extends Parent {
    // ...
  }
  ```
  * cf) 정적메소드 : 클래스에 직접 . 찍고 사용가능
  * super : 부모클래스와 자식의 속성 이름이 겹치지 않기 위해, 부모 클래스의 메소드에 접근할 수 있음.
    - 메소드 오버라이딩
    - 정적메소드 문법 : `super.prop`




> ## 큐, 스택, 트리
### 큐 (Queue)
- 선입선출
### 스택
- 후입선출
- 뒤로가기 : pop()
- 앞으로가기는 어떻게 하게~~~~~?
### 트리




> ## 비동기 프로그래밍
- 코드의 실행순서가 뒤죽박죽
- 브라우저의 JavaScript 코드 실행 과정
- 호출 스택 (Call Stack)
  * 되돌아와야할 코드를 기억 -> stack형태로 기억함
  * 호출스택이 진행되는 동안 브라우저는 먹통이 됨
    - 때문에 호출스택에 많은 기능이 있으면 사용자가 불-편
    - 복잡한 계산을 하지 말아야함!
  * 모든 실행이 끝나야 호출스택이 비워짐 
  * 기다려야할 때가 있는데 호출스택에 채워진채로 기다리면 브라우저는 먹통이 되니까 다른 방식으로 처리해야할 필요성이있다.
    - `작업 큐(Task Queue)` : 기다려야 하는 일을 JavaScript 엔진에서 직접 처리하는 것이 아니라 API를 통해 브라우저에 위임
    - Call Stack(ex.내장함수 - setTimeout)이 Web API 한테 부탁 -> Task Queue : 완료했음 -> Call Stack에 돌아와서 `실행!`
    - 호출 스택이 비워지지 않는다면, 작업 큐에 쌓여있는 작업을 처리할 수 없습니다.
    - 각 작업 사이에 브라우저는 화면을 새로 그릴 수 있습니다.
```js
  setTimeout(() => {
  console.log('hello');
  }, 0); 
  // 작업 큐에 콜백이 추가됨

  console.log('world');
  // 01. console.log('world'); 호출스택
  // 02. setTimeout은 Web API 내장함수 니까 작업큐로 넘어가서 'world' 보다 늦게 실행
  // 호출스택이 비워진 후에 작업큐로 넘어갈 수 있으니까 !!!

  // 03. 호출스택이 기능처리를 담당하지만, 통신, 계산같은 경우 브라우저에서 처리하고, javascript를 통해 부탁하고 받아옴. Queue는 단순히 기억하고 저장! 처리는 Call Stack, Browser / 어쨌든 작업큐를 거쳐서 호출스택으로 최종 실행
```
- 비동기 프로그래밍 (Asyncronous Programming) 기능
  * 어떤 일이 완료되기를 기다리지 않고 다음 코드를 실행해 나가는 프로그래밍 방식
  * 콜백 (Callback), Promise, 비동기 함수 (Async Function) 등이 있음
  * 콜백
    - forEach의 인수로 넘겨준 것 역시 콜백이지만, 이 때에는 콜백이 `동기식`으로 호출됩니다.
  * ` Promise `
    - 콜백의 단점을 해결하기 위해  
    - promise 라는 통에 값이 채워짐
  ```js
  Promise 객체의 결과값을 사용해 추가 작업을 하려면 then 메소드를 호출해야 합니다.
  ```  


# Node.js + HTTP
## 쿠키
- 서버가 응답을 통해 웹 `브라우저`에 저장하는 이름+값 형태의 정보
- 모든 브라우저는 쿠키를 저장할 저장소를 가지고 있음
- 저장소는 자료의 유효기간과 접근 권한에 대한 다양한 옵션을 제공
> 개발자도구 - Application - Cookies
- 브라우저의 `보안`기능 `Set-Cookie Options` - [Back-end영역]
  * 해킹방지를 위해 자바스크립트로 쿠키를 읽지 못하도록 설정해야함 -> 브라우저의 `HttpOnly` 옵션
    - 스크린샷
  * secure : http 접근 ㄴㄴ  
> 자바스크립트에서 쿠키에 접근하지 못하도록 HttpOnly를 항상 설정하는 것이 `best practice` 
- 쿠키 사용 예 : github restAPI -> 인증token을 저장함 (로그인/로그아웃)


# Ajax
> HTTP 복습
>> `C` reate / `R` ead / `U` pdate / `D` elete : POST / GET / PUT,PATCH / DELETE

- 자바스크립트에서 보내는 http 요청
  * GET /api/todos/?title=react 검색기능같이 사용
    - https://glitch.com/edit/#!/sunset-grape?path=.data/db.json:1:0
  * 쿠키를 이용한 로그인, 로그아웃
    - https://glitch.com/edit/#!/salt-hearing?path=.data/db.json:1:0
      * 쿠키가 저장되면 로그인, 쿠키가 삭제되면 로그아웃
      * 근데 우린 이렇게 프로젝트 안할거임(^_^)
  * Cookie vs Token    

# CORS
- Same-origin Policy
  * 다른 탭의 윈도우 객체를 건드릴 수 있다니!
  * 쿠키의 경우에도 동일출처정책이 적용되어있음
```js
 > const child = window.open('http://www.fastcampus.co.kr')
// 새로 열린 웹 페이지의 콘솔에서
> window.foo = 'bar'
// 이전 웹 페이지의 콘솔에서
> child.foo
// 출처가 같다면 접근 가능, 아니면 불가     

// 예를들어 구글 사이트에서 패스트캠퍼스를 열면, 접근 불가능
```
- https://jwt.io/