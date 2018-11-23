# QUIZ
- JavaScript에서는 객체의 속성값을 읽어오거나 속성에 값을 대입하기만 해도 함수가 호출될 가능성이 있다.
- 객체의 속성을 항상 삭제할 수 있는 것은 아닙니다.

# javascript 
- Short-circuit Evaluation(단축평가)
```js
function func1(arg='hello'){
  console.log(arg);
}
func1('') // ''

function func2(arg='hello'){
  arg=arg||'hello'
  console.log(arg);
}
func2('') //hello
```
- 증가 감소 연산자
+ ++ 연산자를 피연산자 앞에 쓰면, 그 표현식은 값을 증가시키고 뒤의 결과값을 반환합니다.
+ ++ 연산자를 피연산자 뒤에 쓰면, 그 표현식은 값을 증가시키기 전의 피연산자를 그대로 반환합니다.
> 같은 부작용(주변환경에 변화를 줌)이 있지만, 다른 결과값을 가진다.
```js
let i = 3;
while (i--) {
  console.log('감소 연산자를 뒤에 쓰면 어떻게 될까요?');
}

let j = 3;
while (--j) {
  // j-=1 / j = j - 1 / --j 같은 의미!!!
  // 앞에다 붙이면 바뀐 결과 값으로 반환되어 시작하니까!!!!
  console.log('감소 연산자를 앞에 쓰면 어떻게 될까요?');
  //감소시킨 후의 결과값 2부터 시작
}
```
- 증감연산자 활용 예제코드
```js
function Counter(initial = 0) {
  this._count = initial;
}

// `this._count`를 1 증가시키면서도 증가시키기 전 값을 반환하는 코드를,
Counter.prototype.longInc = function () {
  const result = this._count;
  this._count += 1;
  return result;
}
// 아래와 같이 짧게 쓸 수 있습니다.
Counter.prototype.inc = function() {
  return this._count++;
}

// ++ 이 뒤에있을 때
   const c = new Counter()
=> undefined
   c._count
=> 0
   c.inc() //반환된 값
=> 0
   c._count
=> 1
   
```
- 연산자 결합순서 : 괄호가 어떤 방향으로 / 계산순서와 다름
```js
//if~else의 삼항연산자
//삼항연산자 : 오른쪽부터 괄호=>, 계산은 왼쪽부터
const num = 1
const str = num === 1 ? (
  'one'
) : num === 2 ? (
  'two'
)
console.log(str);
```
- 값을 비교하는 여러 가지 방법
  + === type 까지 비교 => type이 다르면 무조건 false
  + 사용되는 목적과 사용법이 다름
  + NaN인지 아닌지 => `number.isNaN()`
- Spread Syntax [...arr]
  + 아직 몇몇 브라우저에 이 문법이 구현되어 있지 않기 때문에, 이 문법을 사용하려면 Babel 플러그인 혹은 TypeScript 등의 트랜스파일러를 사용해야 합니다.
  + 배열이 들어가는게 아니라, 배열의 요소가 들어감  
  + `배열을 복사할때도 사용` => 얕은 복사
  + 함수의 인수
  + 앞의 값을 덮어씀
  + 여러개 사용 가능
  + 객체에도 사용 
  ```js
  const obj1 = {prop: 1};
  const obj2 = {...obj1};
  const obj2 = {
    ...obj1,
    c:4,
    d:5 //추가도 가능

    c:5 //마지막에 있는 값이 앞의 값을 덮어씀
    };

  // 이전에는 같은 작업을 하기 위해 `Object.assign` 정적 메소드를 사용했습니다.
  Object.assign({}, obj1);
  ```
    + flatten code
    ```js
  const arr = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
  ]

  function flatten(arr) {
    return arr.reduce((acc, item) => [...acc, ...item], [])
    // return arr.reduce((acc, item) => acc.concat(item), [])
  }

  flatten(arr)
    ```
- 배열의 분해대입 `교재 참고` => 배열의 순서를 바꾸는 알고리즘에 활용해보렴
- 객체의 분해대입 `교재 참고`
  + ({a, b} = {a: 1, b: 2}); => 문장의 첫 글자에 {}이 오면, 블록스코프를 가지기 때문에 ()이 필요
    * 참고
  ```js
  {
    let a = 1
  } 
  {
    let a = 2
  } 
  // 두 a는 다른 스코프를 갖는다.
  ```
  + const print = (x,y) => ({x,y}) : 화살표 함수에서 객체를 바로 반환하고 싶은 경우 `()`로 객체를 둘러싸야함.
  + const print = (x,y) => {x,y} : x,y가 표현식으로 인식 , 결과값 : y
- 매개변수의 분해대입
  + 매개변수에서 객체를 분해대입하는 코드가 많이 쓰이고 이싿.
  + 매개변수에서 필요한 정보가 많은 경우, (=매개변수의 갯수가 많은 경우) 호출할때, 몇번째 매개변수가 어떤 의미인지 알기 어렵다.
  + 그래서 객체의 분해대입을 통해 쓰면 알아보기 쉬움. 순서를 바꿔써도 아무 문제없음. FE Study Class과제에서 매개변수에 {}을 사용한 이유!
    * 객체의 분해대입 예제코드
    ```js

    ```
  + 매개변수의 분해대입 예제 코드  
```js
// 매개변수의 분해대입 예제 코드
// 많이 쓰임!!
function func({prop, array: [item1, item2, item3 = 4]}) {
  console.log(prop);
  console.log(item1);
  console.log(item2);
  console.log(item3);
}

// 1, 2, 3, 4가 차례대로 출력됩니다.
func({prop: 1, array: [2, 3]});

//아래의 코드를 위에처럼 할 수 있다. 
function func(obj) {
  console.log(obj.prop);
  console.log(obj.item1);
  console.log(obj.item2);
  console.log(obj.item3);
}

// 1, 2, 3, 4가 차례대로 출력됩니다.
func({prop: 1, array: [2, 3]});
```  



# 브라우저 측 JavaScript 
- DOM API : 브라우저에 탑재되어있는 기능들 중 하나 / 문서를 조작함
  + 브라우저를 조작한다는 건 DOM API뿐 아니라 다른 API도 있음
- API 에는 굉장히 많은 기능들이 있음. 
- HTML의 계층구조 => 트리
> 요소 선택하기
- el.queryselector() - 특정요소의 자손 찾기도 가능
```js
const divEl = document.querySelector('div')
undefined
divEl.querySelector('.gender')
<select name=​"gender" class=​"gender" required>​…​</select>​
```
- el.closest(selector) : 가장 가까운 조상요소
- el.matches(selector) : true/false 반환
> 요소 내용 조작하기
- el.textContent : text 만 반환
- el.innerHTML : HTML 을 반환
```js
//지향!
// 특히 사용자로부터 입력받은 텍스트를 innerHTML 에 대입해서는 ***절대로*** 안됨!
// HTML로 입력받기 때문에 해킹당하는 경우도 있음. => XSS(Cross=site Scripting)
inputFieldEl.textContent = '<a href="www.google.com">google</a>'
"<a href="www.google.com">google</a>"
// <a href="#">google</a> 자체가 들어감

//지양!
inputFieldEl.innerHTML = '<a href="www.google.com">google</a>'
"<a href="www.google.com">google</a>"
```
> 요소 어트리뷰트 조작하기 : 동적으로 클래스이름을 바꾼다거나 여러가지 작업이 가능함.
- el.hasAttribute(attrName) - 어트리뷰트가 있는지 검사하기
- el.getAttribute(attrName) - 어트리뷰트의 값 가져오기
- el.setAttribute(attrName, attrValue) - 어트리뷰트 설정하기
- el.removeAttribute(attrName) - 어트리뷰트 삭제하기
  * 코드예제
  ```js
  formEl.setAttribute('class','red') // class 를 red로 바꿈
  //But !!! 클래스가 여러개인 경우, 원래있던 클래스가 삭제됨 !!!
  // 그래서 class 어트리뷰트 편집을 위한 속성이 따로 있음
  ```
> 요소 클래스 조작하기 
- el.classList.add(className, ...) - 클래스 추가
- el.classList.remove(className, ...) - 클래스 삭제
- el.classList.contains(className) - 클래스 포함 여부 검사
> 인라인 스타일 조작하기
- `CamelCase로 써준다!`
- el.style.backgroundColor = '#000000'