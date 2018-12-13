# Redux

```
* 핵심 *
- context API 기능
- 고-오-급 상태관리 기법
```
- 상태관리 라이브러리
- React 상태관리 기법 - 내장 상태 : context API
- 80% 실무 프로젝트에 적용됨!
- context API
  * props로 다 ~ 내려주기 어려우니까
  * (비공개) 2018 이전에는 Redux를 통해서 context API를 사용함.
- 값으로 다루면 조합성이 좋아진다.
  * generator, promise, ...
- Redux는 `상태변화`를 값으로 바꿈 
  * 함수를 실행시켜서 코드를 변화시켰지만, Redux는 값으로 바꿔서 변화시킴
    + console.log() 찍기가 쉽다.
    + Undo / Redo => 스택관리가 쉽다.
    + 시간여행 => git log, git commit같은 기능
  * 그렇지 않으면, method로 직접 구현해야함
> ### !Keyword! : store, action, dispatch, subscribe, reducer
- React와는 별개의 상태를 가지고 있음

## Redux 
01. `store`(여러 기능을 갖추고있는 상태 저장소)
  * `state`를 저장하는 저장소
  * 값을 투입하면 state가 바뀜 => react에서는 메소드를 호출하면 상태가 바뀜
  * 투입되는 값 : action
02. `action` (상태변화를 나타내는 값(객체)
03. `dispatch` (action을 store에 파견(디스패치)한다.)  
- React에서 `action이 dispatch될때마다` setState()되도록 해야함.
  * `subscribe` => store.subscribe (상태가 바뀔 때마다 실행할 함수를 등록하는 절차) => `이벤트핸들러 역할!`
  * action이 dispatch될때마다 store에 subscribe해서 state를 바꾼다.
- `reducer` action의 종류마다 상태를 어떻게 바꿀지 Redux에게 알려줘야함
  * 이전상태와 action을 받아서 다음 상태를 반환하는 함수
  * 다음상태를 계산해서 store에 저장

## Redux에서 상태를 바꾸려면?
=> action이 dispatch되면, store는 알아서 이전상태랑 action을 가지고, 상태를 어떻게 변화시켜야할지 입력된 reducer를 통해 다음 상태를 계산함 
  상태가 바뀔 때마다 subscribe를 통해 Redux와 React(setState())의 상태를 바꿔줌.

=> 즉, action이 dispatch됐을때, setState() 할 수 있다!

- `불변성`
  * 내용이 바뀌면 참조가 변하는 성질!


[실습](https://repl.it/@hahn0406/redux-exercise)

# MEMO    