

# MVC(Model-View-Controller)
- MVC 패턴에서 컨트롤러(Controller)는 모델(Model)의 데이터를 조회하거나 업데이트하는 역할을 하며, 모델(Model)의 변화는 뷰(View)에 반영한다. 또한, 사용자는 뷰를 통해 데이터를 입력하는데 사용자의 입력​은 모델에 영향을 주기도 한다.​ 

![simple_mvc](../images/simple_mvc.png)

하지만 대규모 MVC 애플리케이션에서 이 같은 의존성과 순차적 업데이트는 종종 데이터의 흐름을 꼬이게 하여 예기치 못한 결과를 불러일으킨다. 

# Flux
- Flux는 페이스북에서 MVC의 문제를 해결할 목적으로 고안한 애플리케이션 아키텍처이다. Flux 애플리케이션은 크게 세 부분으로 구성되는데, 각각 ​디스패처(Dispatcher), 스토어(Store), 뷰(View)이다. 단, 여기서 말하는 뷰는 MVC의 뷰와는 달리 스토어에서 데이터를 가져오는 한편 데이터를 자식 뷰로 전달하기도 하는 일종의 뷰-컨트롤러로 보아야 한다. ​React를 기반으로 작성된 컴포넌트를 떠올리면 될 것이다.

Flux 아키텍처의 가장 큰 특징으로는 '단방향 데이터 흐름(unidirectional data flow)'을 들 수 있다. 데이터의 흐름은 언제나 디스패처(Dispatcher)에서 스토어(Store)로, 스토어에서 ​뷰(View)로, 뷰에서 액션(Action)으로 다시 액션에서 디스패처로 흐른다.

![simple_mvc](../images/flux_with_action.png)

# 참고
[Flux와Redux](http://webframeworks.kr/tutorials/react/flux/)