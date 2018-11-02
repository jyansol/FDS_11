# Access Token & JWT
- JWT는 한가지 token 형식일 뿐
- 서버개발자에게 `token을 어떻게 포함시켜야하나요?`
- JWT
  * token을 가지고 와서 보내면 되는 것이다.
  * 매번 중복된 설정을 하지 않는 방법 `Axios`

> 더 알아보기
- 서버가 인증토큰을 줌
- 서버는 인증토큰 저장소로 쿠키, 직접관리하는 `local storage` (껐다켰다해도 정보가 날라가지 않음)
  * 쿠키는 저장소, token은 내가 누구인지 나타내는 것
  * token의 유효기간은 만드는 사람 맴
    - 서버에서 언제까지 사용하겠다는 정보를 저장해두고 클라이언트에게 보내고 클라이언트는 포함시켜서 서버에 보내다가 기간이 만료되면 token이 삭제 => ex) token이 만료되었습니다.
  * 휴면계정같은 경우는 token(로그인)과 상관없지만, 법때문에 마지막으로 접속한지 1년 후 서버개발자가 휴면계정이 되도록 설정    
  * 우리는 영원히 로그인이 풀리지 않게 할거지만 실제로 보안관련상 로그인이 풀리게 하는게 좋긴함ㅋㅋ

---

# JavaScript

## Promise 
- '언젠가 끝나는 작업'의 결과값을 담는 통과 같은 객체
- `작업큐`를 사용함. 작업큐를 사용하는 놈중엔 promise, callback함수 등이 있음
```js
//통이 만들어지고
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('2초가 지났습니다.');
    resolve('hello');
  }, 2000);
});

//then을 사용하여 값이 채워졌을때 실행시킬 수 있는 콜백을 만듬
p.then(msg => {
  console.log(msg);
});
//위 표현식의 결과값도 promise다.
```
- then 메소드 자체도 Promise 객체를 반환한다
  * 이 의미는 이런 것도 가능함
  ```js
  p.then(msg => {
  console.log(msg);
  }).then(()=>{
    ...
  })
  ```
  * 콜백지옥에서 벗어날 수 있다. 연이어 비동기작업을 하는 것을 깔끔하게 작성할 수 있다.
  ```js
  const p = new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('2초가 지났습니다.');
      resolve('hello');
    }, 2000);
  });
  //const p의 출력값인 hello가 첫번째 msg -> 첫번째 return 값이 -> 두번째 msg
  p.then(msg => {
  return msg + ' world';
  }).then(msg => {
    console.log(msg);
  });
  //2초뒤에 'hello world' 출력
  ```
- .then()을 연이어 쓴다는 것
  * then 메소드에 넘겨준 콜백에서 promise 객체를 반환하면, 객체의 결과를 따르게 됨
-  setTimeout()으로 작성하게되면 `콜백`이 중첩 중첩 중첩되기 때문에 promise를 이용하면 `비동기 작업`을 연이어 쉽게 할 수 있음
    * cf) 콜백 : 작업큐!!!!!!!   비동기 작업!!!!!!!!
- 값으로 바꾸게 되면 조합성이 좋아짐 / 읽기 좋아짐    
- promise도 값이니까 promise로 이루어지 배열도 가능


## 비동기 함수 (Async Function)
- ES2017에서 도입
```js
// 비동기 함수
async function func1() {
  // ...
}

// 비동기 화살표 함수
const func2 = async () => {
  // ...
}

// 비동기 메소드
class MyClass {
  async myMethod() {
    // ...
  }
}
```
- 비동기 함수는 항상 Promise 객체를 반환한다는 특징을 갖습니다.
```js
async function func1() {
  return 1;
}
func1() //1
// === 
func1().then(console.log); // 1

async function func2() {
  // return Promise.resolve(2);
  return delay(1000,'hello')
  //2초뒤에 hello
}
// func2() //2
func2() // hello
// === 
func2().then(console.log); // 2
```
- 그냥 함수를 쓰면 전부 다 실행되지만 비동기 함수를 쓰게되면 시간?을 설정해 줄 수 있다. `await`
  01. 함수가 기다렸다가 실행됨 => promise가 값이 채워질때 까지 기다림
  01. `await`는 연산자이다. => 채워진 promise의 값을 반환하는 것
      - const str1 = `await delay(3000,'hello')` => 표현식이고 결과값은 hello. 결과값이 str1에 대입
```js
async function main() {
  await delay(1000);
  await delay(2000);
  const result = await Promise.resolve('끝');
  console.log(result);
}

main();
```
- 비동기 함수의 가장 큰 장점은 동기식 코드를 짜듯이 비동기식 코드를 짤 수 있다는 것입니다. 콜백도 없고, .then()도 없음
> 비동기함수 keywords : `async` / `await` / `promise`
- 이전에는 Generator를 이용해 '함수를 잠시 멈춰둘 수 있다'는 특징을 이용해 비동기 함수 처리함 : `yeild`를 사용하면 세밀하게 컨트롤이 가능하나 비동기 함수는 브라우저가 관리함
- 리액트 비동기 처리 : [redux-saga]
- `비동기함수안의 함수에도 비동기 처리해줘야함.`


--- 
# 서버 database

## axios
01. https://www.npmjs.com/package/fds-json-server
    - 실제로 웹에서는 폼을 이용하지만 위 예제는 실습을 위해
    - 사용자 생성은 브라우저 
## json-server


---
# axios 이용한 할일 추가 앱 만들기
- https://codepen.io/jyansol/pen/NEKvMJ
- 상태저장소가 여러개일 경우 상태불일치가 생길 수도 있음 => 상태저장소는 하나만 두는게 좋음!  `single source of Truth`
상태를 한군데만 정해두고 그 저장소를 믿어라!
- 코드중복, 상태중복은 좋지 않음 ㅠㅠ
- cf. 실시간웹(RealTime Web) 
  * 웹소켓 : 내가 정보를 보내지 않아도 요청받을 수 있음. 서버가 계속 연결을 유지함