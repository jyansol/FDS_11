# QUIZ 복습
- console.log(2%3) //2
- Javascript 대소문자 구별
- 예약어(reserved word)란 JavaScript 언어의 기능을 위해 미리 예약해둔 단어
  * https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Lexical_grammar#Reserved_keywords_as_of_ECMAScript_6


# Javascript  
- to do list 버그
> https://codepen.io/jyansol/pen/EdwzOQ
- mouseover, mouseout이벤트는 직접 이벤트를 걸지 않은 자식 요소까지 이벤트가 발생하고 bubbling이 일어남, mouseenter, mouseleave이벤트는 자기 자신에게 마우스포인터에 대해 발생, bubbling이 일어나지 않는다.
- 동적구현
  * 01. DOM 객체를 직접 넣어서 createChild / removeChild / appendChild......?
    - 실제로 몇개를 추가/표시해야할지 모르는 경우
  * 01. 스타일을 다르게 먹여서 display : none; => display : block;
    - 정확히 무엇인가를 표시해야하는지 아는 경우


# 해커톤 관련
- npm run build : html,css 압축
- npm start : 개발용 code가 바뀔 때 마다 새로 build된 결과물을 빠르게 보여줌
- 한명이 저장소 생성 > 접근권한 부여                                                                                                                                                             


# git 협업시 개행문자 주의사항
- autocrlf
> git config -- global core.autocrlf
- merge conflict 병합충돌