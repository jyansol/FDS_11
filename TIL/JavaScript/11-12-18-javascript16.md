# MEMO
### 통신, 알고리즘
- ES2015 모듈 / React 빌드 도구의 CSS 모듈
### 코드가 복잡하다
- 서로 연관된 htrml, css, js => `component`
  * 예를들어, 상품목록관련된 파일들을 한 컴포넌트에 작성
### 코드의 중복 (`횡단관심사(cross-cutting-concerns)`:여러부분에 걸쳐 항상 적용이 필요한 기능 )
- ! 고차함수 !
- 레이아웃
- 로그인 아닐때
- 로딩 인디케이터
- 버블링, 캡쳐링
> 이런 문제들을 해결합시당

# React

https://codepen.io/jyansol/pen/jQMJrZ?editors=0010

https://codepen.io/jyansol/pen/xQRKVY

- `선언적`이고, `효율적`이며, 유연한 JavaScript 라이브러리
- `선언적` : 코드가 생긴대로 결과물이 나옴, 코드가 결과물의 구조를 잘 반영하고 있음
  * html : 동작순서 x 
- `효율적` : rootEl을 비웠다가 다시 그려주는 방법은 기계에게 비효율적 
  * react는 사람이 새로그리는 것처럼 작성하고, 기계에겐 효율적인 코드로 변환
- `유연함` : UI를 값으로 담을 수 있다. UI를 반환하는 rander() 메소드를 가지고 있다. 
  * 값(뷰) : 무엇을 그릴지에 대한 설명, ( = 리액트 엘리먼트 )
  * JSX 문법 => 사실은 React.crateElement() 라는 코드 입니다. `객체`가 반환된다! DOM API도 객체였음
  - cf. 명령형 : 결과물의 최종적인 구조를 확인하기 어려움. 코드를 해석해야 결과물을 알 수 있음. 
  * DOM API
- JSX 중괄호 안에는 어떤 JavaScript 표현식도 넣을 수 있습니다.
```js
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        // textContent같이 작동
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}
```  
  * 우리는 전체 쇼핑 목록을 그리기 위해 `<ShoppingList />`와 같이 쓸 수 있습니다.
- 컴포넌트 vs 엘리먼트
  * 하나의 컴포넌트로부터 수많은 엘리먼트가 생성될 수 있다.
- 자식 컴포넌트에서 부모 컴포넌트로 직접 정보를 줄 수 없음. props는 부모로부터 자식에게    
- 컴포넌트는 상태를 가질 수 있고, 바꿀 때 .setState()를 통해서만 바꿀 수 있다.
- .setState() : state의 내용을 바꿔주는 기능(상태변경) / 화면을 다시 그리는 기능(화면갱신) => 반드시 이 메소드를 통해 바꿔야함
- 상태로부터 화면이 자동으로 그려짐 화면을 다시 그리기 위해서는 상태를 바꿔주는 방법밖에 없고 그 메소드는 .setState()란다
- `상태끌어올리기!` : 상태를 바꾸는 함수를 만들어 자식에게 내려준다.
- 리액트 엘리먼트 하나만 반환할 수 있다.