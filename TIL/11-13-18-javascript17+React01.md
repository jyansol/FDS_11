# React
- [리액트의 구조를 알아보자](https://codepen.io/jyansol/pen/jQMJrZ?editors=0110)
- 컴포넌트와 엘리먼트(return 아래의 코드)는 다르다!
- board는 square한테 props을 줄 수 있지만, 반대는 안됨
- `화면을 그리기 위해서 상태를 바꿈`
- props는 객체의 속성


## JXS
- 자바스크립트의 확장 문법
- DOM attributes 문법이 html이랑 다르다!
  * camelCase
- DOM 요소객체를 생성하는데 비용이 많이듬. 대신 React는 객체니까 생성비용이 아주아주 적게듬. 
- React DOM이라는 라이브러리가 우리를 대신해서 DOM에 appendChild해쥼
- `<div id="root"></div>` “루트” DOM 노드
- React로 구축한 어플리케이션은 보통 하나의 루트 DOM 노드를 가집니다. React를 기존 앱에 통합하는 경우, 원하는 만큼의 여러 루트 DOM 노드를 만들 수도 있습니다. => 그러나 보통 하나의 루트 DOM 노드만을 사용함
- `React element` VS `React Native`
- React 요소는 변경 불가능 합니다. 한번 요소를 만들었다면, 그 자식이나 어트리뷰트를 변경할 수 없습니다. => 불변성(Immatability)
  * 값을 변경하고 싶을때는 값을 새로 만든다.
  * 배열이나 객체안의 값을 변경하고 싶을 때는 바로 변경했지만,
    slice()처럼 마치 불변인 것처럼 씀.
  * React는 객체니까 변경가능 : React에서의 불변성은 변경할 수 없다뜻이 아니라 `처음부터 싹- 새로만든다는 의미`
- 화면을 바꾸는 코드를 짠 적이 없음. 상태로부터 화면이 어떻게 그려지는지 => render() 메소드를 다 다시 호출해보고 화면을 다시 그림
- setState()
- React는 꼭 필요한 부분만 갱신 : React DOM은 요소 및 그 자식을 이전 버전과 비교하고, DOM을 원하는 상태로 만드는 데 필요한 DOM 업데이트만 적용합니다.
- todolist 예제
  ```js
  textContent = '' 
  textContent = '롸'
    ```
    비효율적!
    React는 진짜로 변경된 부분만 고쳐줌
- 이전의 화면과 지금 그려야할 화면을 비교해서 변경된 부분만 그려줌


## 컴포넌트와 props
- 컴포넌트를 조립
- props는 부모로부터 받은 데이터일뿐 수정할 수 없다. (수정/삭제ㄴㄴ)
```js
function withdraw(account, amount) {
  account.total -= amount;
}
// 입력이 변경되므로 옳지않음!
```
- 우리가 render() 컨트롤 할 수 없기 때문에, `props에 대해 순수 함수`처럼 동작해야함
```js
function sum(a, b) {
  return a + b;
}
``` 


## State와 라이프사이클
- 캡슐화 : 정보를 숨기는 행위 => 정보가 캡슐화 되었다!
- 화면을 다시 그리고 싶으면 무조건 state가 필요함
- 내가 기억하고 있는 상태를 업데이트
- 클래스에 `라이프사이클` 메서드 추가하기
  * 화면에 표시될 때 setInterval, 사라졌을 때 clear
  * `mounting` : 어떤 컴포넌트가 DOM에 최초로 렌더링되는 사건
  * `unmounting` : 렌더링됐던 것을 삭제하는 사건
  ```js
  // 라이프사이클 훅 메서드 : 특정 시점에 실행될 함수를 걸어놓는 느낌!

  // 1. 컴포넌트를 렌더링
  componentDidMount() {
  }
  // 2. 컴포넌트가 unmount되기 직전에 {} 의 코드가 실행
  componentWillUnmount() {
  }
  ```
  * 컴포넌트가 태어나서 돔에 장착됐다가 죽는..그...런..ㅠㅠ
  * 다른 것도 있긴한데 위 2개를 가장 많이 씀
  * componentWillUnmount() 해주지 않으면 화면에 없는데 업데이트해야해서 오류남 ex) 뱀게임
- State 바르게 사용하기
  * 객체이므로 this.state.comment = 'haha' 로 변경할 수 있지만 화면을 다시 그려주진 않음.
  * `setState()` : 비동기 함수, 바로 state가 바뀌지 않고, 나중에 바뀜. 부탁하고 넘어감. 
```js
  handleInc(){
    this.setState({count: this.state.count+1})
    this.setState({count: this.state.count+1})
    // 이렇게 작성해도 count가 2가 되지 않음.
    // 다음 state를 작성할때 이전 state를 신뢰하면 안됨.
    // 비동기 함수이기 때문에 부탁하고 바로 넘어감.
  } 
```
  * 대신 비동기 콜백을 이용해야함
    - 다음상태를 이전 상태로부터 계산해내고 싶을때는 setState안에 함수를 써줘야함.
```js
  // Correct
  this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
  }));
```

  - 이렇게 작성해야함!

```js
  handleInc(){
    this.setState(prevState => {
      return {
        count: prevState.count + 1
        // count의 초기상태는 0
        // react에 상태업데이크 '큐'가 있고 차례대로 실행
      }
    })
        this.setState(prevState => {
      return {
        count: prevState.count - 1
      }
    })
  } 
```
-`Object.assign()`은 얕은 병합 : 객체안의 객체, 배열안의 배열 지양!


01. 화면
01. 상태설계
01. 상태로부터 화면그리기
01. 상호작용이 일어났을때 화면을 그려주는 코드

// score, problem, 몇번째가 정답이지 기억
// 상태설계 this.state
// 상태로부터 화면 그리기
// 상호작용이 일어났을때 화면을 그려주는 코드

` rgb 챌린즤 `
https://codesandbox.io/s/llx1v8p5j7

- 비동기함수를 이벤트 리스너에 등록하는 것이 위험함.
이벤트 리스너가 여러번 사용되는 경우 1번이 실행되는 동안 2번이 실행되면서 e.target이 내가 원하지 않는 것을 참조하는 경우가 생김 => `event.persist()`
- 근데 event.persist() 보다 다른 방법을 쓰는게 더 좋음
- 필요한 속성을 이벤트객체로부터 미리 다 빼놓는 방법이 있음



## JSX 콜백에서 this
- onClick 에 handleClick을 쓰면, 그 함수에서 가르키는 this가 무엇인지 모름
- .addEventListener 
- 엄격모드가 아닐때에는 this
- 엄격모드 this : 전역객체(window) -> window에는 setState라는 속성이 없자나여
> 해결책 : 근데 이 방법 실무에서 잘 안사용함
  >> 해결책 : 화살표함수를 쓰자!!!!!!!!!!!!!
```js
//해결책01
this.handleClick = this.handleClick.bind(this);
//해 결 책 ! 화살표함수의 this ! ! ! ! ! ! \(^0^)/
//이벤트 리스너가 보이면 화살표함수를 쓴다!!!!!!!!
<button onClick={()=>this.handleClick()}>
```
- 생성자 내부에서의 this는 제대로된 인스턴스
- 그 인스턴스를 this.handleClick에 저장

## 조건부 렌더링
- if()를 사용해서 가능함
- && 논리 연산자를 사용해 if를 인라인으로 넣기
> 예시
```js
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}
```
- 컴포넌트가 렌더링 되지 못하도록 방지



---

# JavaScript 
## 예외처리

> ### 동기식코드
01. try / catch
```js
try {
  console.log('에러가 나기 직전까지의 코드는 잘 실행됩니다.');
  // 여기까지 실행되고 에러를 만나면 catch로 넘어감
  new Array(-1); // RangeError: Invalid array length
  console.log('에러가 난 이후의 코드는 실행되지 않습니다.');
} catch (e) {
  console.log('코드의 실행 흐름이 catch 블록으로 옮겨집니다.');
  alert(`다음과 같은 에러가 발생했습니다: ${e.name}: ${e.message}`);
}
```
 *  try 블록은 예외 처리를 위해서만 쓰이는 것은 아닙니다.
 *  try 블록 바로 뒤에 finally 블록이 오면, finally 블록에 있는 코드는 try 블록 안에서의 에러 발생 여부와 관계 없이 무조건 실행됩니다.
 ```js
 for (let i of [1, 2, 3]) {
  try {
    if (i === 3) {
      break;
    }
  } finally {
    console.log(`현재 i의 값: ${i}`);
  }
}
// break가 작동되지만, finally가 실행되고 나서 빠져나감
```
* try + catch (에러를 만나면) + finally
* prompt는 문자열을 받아오기때문에, parseInt 처리!
02. 직접 에러 발생시키기
 - new Error('인스턴스를 만든거임,설명');


 > ### 비동기식코드
 01. 비동기 콜백 (비동기 종류중 하나인 콜백!)
 - 비동기식 코드는 try / catch로 잡을 수 없음
 - JavaScript 엔진은 에러가 발생하는 순간 `호출 스택을 되감는 과정`을 거칩니다.
    * func1(){ func2() } / func2(){ func3() } / func3(){ err } 하지만, func1을 호출해도 에러를 발생
```js
function func1() {
  try {
    setTimeout(() => {
      throw new Error('에러!');
    });
  } catch (e) {
    console.error(e);
  }
}
func1()
// 실행되는 동안에는 err없음. 브라우저에게 부탁하는거니까
// 호출 스택을 따라 올라가도 try 블록을 만나는 것이 아니므로, 코드의 실행 흐름이 catch 블록으로 옮겨지지 않는 것입니다.
// 비동기 코드(나중에 실행되는 코드)에 둘러줘도(바깥) 소용없음
```
- 콜백 안에 작성해야함 => `콜백에 에러를 잡는 예`
```js
setTimeout(() => {
  try {
    throw new Error('에러!');
  } catch (e) {
    console.error(e);
  }
});
```

02. Promise : 작업을 실패해도 promise안에 기록
- then 메소드의 연쇄 안에서 에러가 발생하면, try...catch 구문과 유사하게 처음 만나는 에러 처리 콜백으로 코드의 실행 흐름이 건너뛰는 결과를 낳게 됩니다.
  * 다음 then이 실행되는게 아님
- 비동기함수안에서 rejected인 경우(rejected promise인 경우) await하면 try / catch로 잡아낼 수 있다. 
- 동작방식은 복잡하나, 사용하기에는 비동기함수가 좋다! 
> 사용자가 이상한 코드를 입력해서 받아온 경우 예외처리를 할 것임
> 비동기함수를 쓴다면 어느경우든 try / catch를 써서 에러를 잡을 수 있음