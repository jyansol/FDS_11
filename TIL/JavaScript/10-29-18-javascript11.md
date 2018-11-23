# 코드의 복잡성 낮추기
  - 유지보수를 위한 코드 작성
  - 주석 작성
  - 클래스, 함수 사용
# HTTP
  - HTTP : 어떻게 통신하는지에 대한 의미
  - REST API : 
# Node.js   
  - Postman : web 주소를 입력해서 내용 + 요청 을 받아봄.
  - https://developer.github.com/v3/#authentication
    * github 에서 token 생성
  - Node.js modules
    * DOM API와 다름!
    * 브라우저에는 없는 node.js 기능 
    * require()
    * `node` > `const name = repuire('./name')` > `name`
  - npm init -y :  npm으로 관리하는 파일을 실행하겠다. 
    * package.json 파일 생성 
  - npm install sweetalert 
  - rm -rf node_modules 해도 package.json 에 무엇을 설치했었는지 남아있음 > npm install
  - npm run `start`
  - npm 에서 download
  - Request Methods : https://developer.mozilla.org/ko/docs/Web/HTTP/Methods
  - <a href="#idname"> / <h1 id="idname"> -> browser 내장 기능
# express : 서버 코딩을 쉽게 해줌
  - FOO=BAR node : 환경변수지정 > process.env.FOO 환경변수 불러오기


# JavaScript
- 분해대입!!
- 배열처럼 동착하는 iterable 객체
## Generator 함수 : 비슷한 루프를 돌기위한 함수
```js
function* numberGen() {
  yield 1;
  yield 2;
  yield 3;
}

// 1, 2, 3이 순서대로 출력됩니다.
for (let n of numberGen()) {
  console.log(n);
}
```
: Generator 함수 안에서는 yield라는 특별한 키워드를 사용할 수 있습니다. Generator 함수 안에서 yield 키워드는 return과 유사한 역할을 하며, iterable의 기능을 사용할 때 yield 키워드 뒤에 있는 값들을 순서대로 넘겨줍니다.
- yield* 
- 루프를 `값`으로 만들 수 있다 => 초합, 변경이나 추가 작업이 가능