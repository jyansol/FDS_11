# JavaScript

##모듈
https://codesandbox.io/s/llx1v8p5j7
- require.js / Browserify => 자바스크립트를 여러 파일에 나눠 작성하기 위한 구닥다리? 모듈 시스템
- commonJS(require(): node.js모듈 시스템에서 쓰임), UMD(define()) => 기존 자바스크립트 활용해서 모듈 시스템을 자체적으로 만들어냄
- ES2015부터 모듈시스템을 위한 새로운 문법이 생김 => `type="module"` => 아직 사용하진 않음
- import 혹은 export
- 모듈 스코프
  * 여러 모듈의 가장 바깥쪽에서 같은 이름으로 변수, 함수, 클래스를 선언하더라도, 서로 다른 스코프에서 선언되기 때문에 이름의 충돌이 생길 일이 없습니다.
  * import / export로 다른 모듈에 정의된 값, 이름을 사용할 수 있다.
  * export { foo, spam }; => import { foo, sapm } from "./variables.js";

## 선언과 동시에 export 하기
- 선언부 앞에 export 붙이기 => 변수를 export, 값을 export하지 않음

## default export
- 값을 받을 변수를 import하기 때문에 import의 foo에는 사용하고싶은 이름을 사용할 수 있다.
- 하나의 모듈에서 default 
- export default 'bar'; => import foo from './foo.js'
```js
// add.js
export default function(x, y) {
  return x + y;
}
// index.js
import myAdd from "./add";
```
  - class도 값이기 떄문에 익명 클래스만들기가 가능하다.
```js
export default class myComponent {
  render ()
}
```
- import 구문에서 default export와 일반적인 export를 동시에 가져올 수 있습니다.
```js
import React, { Component, Fragment } from 'react';

// 한 파일에
export default class {}
export const Component = "..."
export const Fragment = "..."
```
- 다른 이름으로 import 
  * import { foo as FOO } from "./variables";
  * 모듈간의 이름 충돌이 있을 때 사용
- 같은 모듈을 여러 다른 모듈에서 불러와도, 모듈 내부의 코드는 단 한 번만 실행됩니다.




# React
## 컴포넌트 여러개 렌더링
## key
  키 설정 : `배열`을 그릴 때 `키`가 꼭 필요함
- cf. div를 그린다고 할때 키가 필요 없음
- 배열에 들어있는 요소마다 식별자를 키(다 다른 값)로 넣어주세요.
- 배열 인덱스를 키로 사용할때 조심해야함 => [0] [1] 사이에 그려줘 - React는 [1] 의 내용을 바꾸고 [2] 를 추가함 - 상태를 갖고있는 경우라면 난리남
- map()에서 반환되는 엘리먼트에 키를 넣어줘야함
- `키는 React에게 힌트를 제공하지만 컴포넌트로 전달되지는 않습니다.` => key 라는 props를 쓸 수 없음!
  * key, ref는 component의 props로 쓸 수 없음
```js
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```
  - 배열이 아니어도 key를 줄 수 있음 - key가 바뀌면 상태도 함께 사라짐 - `상태초기화` 
## class : 객체를 만들기 위해
- instance를 React가 생성 - 그 instance에 state가 들어있음 this.state, this.setState() 등으로 쓰는 것이 class의 instance를 만지는 거임
- 화면을 어떻게 그리느냐에 따라서 Nodestate가 달라짐
- statte가 계속 유지되는 것이 아님
## State
- App>Game 대신 App>TankBoard를 그릴때(Game이 화면에서 지워질때), Game의 state는 기억속에 삭제됨
- 함수형 컴포넌트는 상태를 가질 수 없다. instance가 생성이 안되니까 ! class가 아니니까 !
- 함수형 컴포넌트에도 상태를 기록할 수 있는 기능이 추가되고...ㅇ...ㅣㅆ....ㄷ....ㅏ.............
- 화면에 그려져야! 상태를 가질 수 있음!

## onChange 제어되는 컴포넌트
- 화면을 그리는 기능만을 갖게함, 다르게 표시하고 싶다면 `상태`를 바꿔라!
- 사용자의 입력을 세밀하게 제어하고싶고, 바로 피드백을 주고 싶은 경우
- 추가작업이 필요함 (value, 함수) => `formik` 라이브러리
- 제어되지 않는 컴포넌트를 사용하려면, DOM 객체를 가져와야함 근데 querySelector로 가져올 수가 없음 ㅜ.ㅜ => `ref`를 사용해서 DOM 객체를 가져올 수 있음
### Form
- HTML 폼(form) 요소는 그 자체가 내부 상태를 가지기 때문에, React에서는 다른 DOM 요소들과는 조금 다르게 동작합니다. 
- TML에서 <input>, <textarea>, <select> 같은 form 요소는 자기만의 상태를 가지고 사용자의 입력에 따라 업데이트됩니다. 반면에 React에서는, 변경 가능한 상태를 일반적으로 컴포넌트의 state 속성에 위치시키며, 이는 setState()로만 업데이트할 수 있습니다.
  * 서로 다른 state가 있고, 상태 업데이트 방법이 다르기 때문에 제어되는 컴포넌트가 필요함. => `진리의 유일한 원천`
- 제어되는 컴포넌트
  * input.value를 넘길때 value props에 값을 함께 넘겨주면 더이상 값을 입력할 수 없다.
  * 마치 바로 입력이 되는 것 처럼, input의 내장 기능을 없애고 그 값으로 상태를 그려주고 보여줌
      - https://codepen.io/jyansol/pen/yQMejw?editors=0010
  * 이를 통해 사용자 입력을 수정하거나 검증하는 것이 간단해집니다. 예를 들어 모든 유저의 이름을 강제로 대문자로 받거나 숫자만 입력가능하게 할 때
### textarea 태그
- DOM 세계에서는 사용법이 다르지만, 리액트세계에서는 Form처럼 onChange를 사용해서  
### select 태그
- https://codepen.io/gaearon/pen/JbbEzX?editors=0010
- <select value={this.state.value} onChange={this.handleChange}> //지금 선택된 옵션의 value값
- onChange={this.handleChange} props를 사용해야함, 이것을 지우면, 안바뀜!

## State 끌어올리기
- 여러 자식들이 공유해야할 상태가 필요할 때

## 합성 (composition) vs 상속 (inheritance)
- `상속 ㄴㄴ 조합 ㅇㅇ`
- FancyBorder의 아래 코드가 `props.children`이라는 특별한 props가 있음
  * https://codepen.io/jyansol/pen/ZmeWeQ?editors=0010
- props로 받은 엘리먼트를 자식에서 그릴 수 있음  





## 컴포넌트 하나에 파일 하나
