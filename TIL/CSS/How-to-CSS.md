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


---
# 정리
- BEN을 쓴다는 것은, 이름충돌을 사람이 해결해야함 => 특정 컴포넌트와 관련된 파일을 만들자 => PostList.scss => PostList.js 에서 import해서 사용한다