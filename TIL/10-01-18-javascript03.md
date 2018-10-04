
# QUIZ
- `parseInt`, `parseFloat`
  + 문자열을 number 타입으로 바꾸기 위해 parseInt 혹은 parseFloat 함수를 사용할 수 있습니다.
```js
parseInt('123'); // 123
parseInt('110', 2); // 6 (문자열을 2진수로 간주한다.)
parseFloat('12.345'); // 12.345
parseInt('hello'); // NaN
```

# JAVASCRIPT 

- typeof 연산자
- null : 객체가 없다는걸 나타내는 용도로 사용
```js
typeof null //object
```
- 변수가 선언한적 있는지 없는지
```js
typeof foo //undefined => 선언한적 없음
```
- null VS undefined
  + 명시적으로 없음을 나타낼 때 `null` 사용
  + undefined : 비록 undefined가 '없음'을 나타내는 값일지라도, 대입한 적 없는 변수 혹은 속성과, 명시적으로 '없음'을 나타내는 경우를 구분을 할 수 있어야
- 드 모르간 법칙!
- Null Check!
```js
// 아래 세 개의 식은 완전히 같은 의미입니다.
input !== null && input !== undefined;
input != null;
input != undefined;
```
  + null check를 할 때 만큼은 `==`를 쓰는 것이 편리합니다.
  왜냐하면,
```js
null === undefined; // false
null == undefined;  // true

null == 1       // false
null == 'hello' // false
null == false   // false

undefined == 1       // false
undefined == 'hello' // false
undefined == false   // false
``` 
이기 때문입니다.

- 매개변수와 인수
- x와 y는 별개 => 변수를 넘겨서 함수에 대입할 일은 절대 없음.
```js
function reassign(x) {
  x = 2;
  return x;
}

const y = 1;
const result = reassign(y);
//표현식의 값(y)가 넘어감

console.log(y); // 1
console.log(result); // 2
```
- return 구문이 실행되면 함수 즉시 실행 + 종료
- jsp 함수는 항상 값을 반환하는데 만약 ruturn 구문이 없다면 `undefined` 반환
- Scope 스코프 : 변수의 유효범위
  + `함수에서 매개변수`는 `함수가 실행되는 동안`에만 `유효`함.
  + `매개변수는 함수 스코프를 가진다.`
  + 중첩된 스코프 안에서는 바깥의 정의된 스코프를 사용할 수 있다. 
    => 부모의 부모 ... 부모 접근가능 / 사촌은 불가능
- 변수 가리기 (Variable Shadowing)
```js
const x = 3;
function add5(x) { 
  // `x`라는 변수가 다시 정의됨, 전역변수 x와 별개의 변수 => 그래서 변수가리기 라고 함!
  function add(x, y) { // `x`라는 변수가 다시 정의됨
    return x + y;
  }
  return add(x, 5);
}
add5(x);
```

- 익명함수
```js
function isEven(x) {
  return x % 2 === 0;
}
[1, 2, 3, 4, 5].filter(isEven); // [2, 4]

//위의 함수를 재사용할일이 없을때, 익명함수를 많이 사용함.
[1, 2, 3, 4, 5].filter(function (x) {
  return x % 2 === 0;
}); // [2, 4]

//화살표함수로 바꾼다면
[1, 2, 3, 4, 5].filter(x => x % 2 === 0);
```

- function keyword 함수
  + return 반드시 필요함

- 화살표함수
  + return 생략 가능
  + 익명함수 밖에 없음
```js
//화살표 함수
const add = (x, y) => x + y; 
add(3,3); //6

//function keyword 느낌처럼 쓰고싶다.
const add = (x, y) => {
  //여러 구문
  //return도 가능
}; 

// 매개변수가 하나밖에 없다면, 매개변수 괄호생략 가능
const negate = x => !x;
```  

- 제어문
  + 중괄호(curly brace) 내부에 들어있는 구문이 하나라면, 중괄호를 생략해 줄 수도 있습니다.
  + `지양함` => 유지보수힘듬
```js
  if (result === 6) alert('당신은 운이 좋군요!');
```  

- swich문
  + 의도적으로 break 생략
```js
case 'purple':
    case 'violet':
      // 이 코드 영역은 english 변수의 값이 'purple'일 때와 'violet'일 때 모두 실행됩니다.
      result = '보라색';
      break;
```     
- while VS do...while 구문
- 배열의 순회 방법
```js
//01. for
//02. forEach
//03. for ... of
const arr = [1, 2, 3, 4, 5];

for (let item of arr) {
  console.log(`현재 요소는 ${item} 입니다.`);
}
```
- braak / continue : 가장 가까운 루프에 대해서만 효과를 가짐
  + `break;` : 루프 밖으로 나가고 싶을 때!
  + `continue;` : 나머지 코드를 실행시키지 않고, 루프 처음으로 돌아감
- 함수 즉시 종료하기
  + return : swith에서 break 없이 return 사용가능.  