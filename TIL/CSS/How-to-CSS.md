# CSS 방법론
- [CSS방법론](http://wit.nts-corp.com/2015/04/16/3538)
- scope가 있는 것 처럼 코딩을 하자!


## BEM (Block, Element, Module)
- class 작문법
  * ex) header__button, .block-name__element-name => 언더바 2개!
- Modifiers : 상태가 있을 때
  * .block‐‐modifier {…}
  * .block__element--modifier {…}   
- `React에서는 .Component__name`
- 단점 : 근데 코드가 길어져서 차세대 방법은 아님 
- 장점 : 유지보수하기 쉬움


## SASS
- [사용방법](https://sass-lang.com/guide)
- 두 가지 문법 : `Sass`, `SCSS`
- npm install node-sass
- Nesting
  * &(자기선택자)를 사용하면, 부모에 대한 내용이 빠지고, 상위 `문자열`이 들어감
  * 자기선택자를 안쓰면, 부모자식관계로 형성
  ```scss
  .PostList {
    &__title {
      color: $main-color;
    }
  }
  // body의 loading의 자식인 자기자신(option)
  .option {
    body.loading & {
      color : red;
    }
  }
  ```
- Import
  * CSS에서 import하면 속도가 느려짐, 통신을 한번 더 해야하니까
  * Scss에서 import하면 컴파일 과정에서 다 합쳐짐
  * 여러파일에서 공유해야하는 변수
- Mixins (공유되어야하는 `코드` 뭉치(JavaScript의 함수))
  ```scss
  @mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
  }
  .box { @include transform(rotate(30deg)); }
  ```
- 값을 재사용하고 싶을때는 `변수`, 코드를 재사용하고 싶을때는 `Mixins`
  * 클래스명으로 그 부분에 역할과 책임을 나타내고 싶을 때 => 클래스 이름을, 되도록 한 요소에 클래스 이름을 그 엘리먼트에 해당하는 이름만 붙여두고 싶음 => 예를들어 PostList__title과 같이 명확히 나타냄
  * 스타일이 공유되어야 하는 부분은 `Mixins`로
- Operators


# 정리
01. BEN을 쓴다는 것은, 이름충돌을 사람이 해결해야함 => 특정 컴포넌트와 관련된 파일을 만들자 => PostList.scss => PostList.js 에서 import해서 사용한다
01. CRA
- [CreateReactApp](https://facebook.github.io/create-react-app/docs/adding-a-stylesheet)
- Adding a CSS Modules Stylesheet
  * 유일하고 식별가능한 이름을 `자동`으로 만들어 줌
  * scss파일에서 className은 camelCase로 작성해서 `.표기법`으로 접근한다.
- PostForm을 edit랑 new일때 사용되는데, 스타일이 조금 다를때
  * Editing={true}라는 prop
  * CSS module을 쓰면서 className을 동적으로 구현

---
---
---

# UI Framework - UI for React
- framework를 사용할때, React version이 있는지 확인하고 쓰면 좋습니다!

## semantic-ui-react
- [React-semantic-UI](https://react.semantic-ui.com/)
- 여러가지 컴포넌트를 제공함
- import가 적용된 `try it`소스를 복붙하면 됨!
- npm install semantic-ui-react => npm install semantic-ui-css
- iindex.js => import 'semantic-ui-css/semantic.min.css'; 연결!

## reactStrap
- [reactStrap](https://reactstrap.github.io/)
- Scss / 커스터마이징이 쉽다.

## semantic-ui
- [semantic-ui](https://semantic-ui.com/)

## bootstrap
- [bootstrap](https://getbootstrap.com/)
- html code에 쓰기 쉽게


---
---
---

# Component DEMO page build 도구
- [Storybook](https://storybook.js.org/)
- `npm run stotybook`
- style cording할때 쓰기 좋음
- Loading stories dinamically
  * storybook폴더안의 config 파일 수정
  ```js
  import { configure } from '@storybook/react';

  const req = require.context('../src/components', true, /\.stories\.js$/);

  function loadStories() {
    req.keys().forEach((filename) => req(filename));
  }

  configure(loadStories, module);
  ```
- 컴포넌트안에서 작성하면 편하잖아요 ? 
  * components 폴더에 `PostForm.stories.js` 파일 생성 => stories 폴더의 index.js 내용을 복붙
  * components를 import하고 .add()에 호출

- storybook을 사용하려면 create-react-app이 설치되어있는지 확인하고, build config를 가져오는데, window에서는 간혹 그러지 못하는 이슈가 있다. => 가짜 config 설정
- `CSS와 관련된 test만 할 것!` => 부작용이 없는 component
  * component를 분리할때, 기능과 Form으로 나눈부분이 storybook 사용 시 장점이 될 수 있음 => `역할과 책임을 분명히 하라!(PC vs CC)`
    + PC folder / CC folder / stroybook
    + > !important `언제 container 컴포넌트를 작성해야 하나요?`
  * [컴포넌트 작성법](https://medium.com/@seungha_kim_IT/presentational-and-container-components-%EB%B2%88%EC%97%AD-1b1fb2e36afb)
- 분해대입 error
  01. comsumer의 기본값  - React.createContext(`{}`) : provider가 없을 때 기본값을 사용함
  02. UserConsumer를 다른 파일로 빼주는 것

---
# To Do List
- input tag 에게 Ref를 내려주고 싶을 때, innerRef로 내려 줄 수 있었다. 그런데 사용법이 바뀐 것 같다.
- 배포/SEO관련