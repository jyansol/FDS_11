# QUIZ

- polyfill : 특정 기능이 지원되지 않는 브라우저 상에서 기능을 구현하는 코드를 일컫는 용어
- ul ~ p { color: red; } : ul 요소 뒤에 오는 형제레벨의 모든 p 요소의 텍스트를 붉은색으로 표시한다.
- 마진병합현상 : margin이 큰값이 적용
- em / rem
- border-box는 border 값까지 넓이로 가지는 박스를 만드는 속성이다.
- 웹접근성
  + 메뉴를 건너뛰고 본문으로 바로 갈 수 있는 기능이 있어야 한다.


  # javaScript

- javascript 언어 + 브라우저사용법(구동환경)
- repl에 node 어쩌구 뜨면 안됨
## best practice : 좋은 관례 
01. var 대신 let, const
02. const 만 쓰는 것! : let을 사용하면 의도치 않게 다른 값이 대입되어 버리는 일이 생길 수 있기 때문
03. 식별자는 영어로!
04. CamelCase
05. === vs ==(타입이 달라도 같게봄)
06. Number.isFinite(1);
07. number 타입과 다른 타입의 연산은 웬만하면 피하는 것이 좋습니다.



```js
const obj = {
  x : 0,
  y : 1
 }
 ```
// 'y' 속성이름 부분에 문자열이 원칙 => y 로 표기해도됨.
// 속성값으로 함수, 객체가 올 수 도 있음.
// obj.y.x 객체의 객체의 값을 불러오는 리터럴
// 속성값 바꾸기
```js
obj // x : 0 , y : 1
obj.x = 3 // x : 3
obj.x // x : 3
```
// delete 연산자
```js
delete obj.x; 
// x 값을 삭제
```




- 메소드 : 속성으로 불러와서 함수 호출
// 어떤 객체의 메소드안에 this가 있으면 그 this는 '메소드가 호출될 때' 해당 객체를 가르킴
```js
const obj = {
  x: 0,
  increaseX: function() {
    this.x = this.x + 1;
  } 
  // this : 자기자신 = obj
};

obj.increaseX();
console.log(obj.x);
```






- 배열
//.을 통해 호출하는 함수 => 메소드
```js
const arr = [1,2,3]
arr.push(4);
arr.push(5);
arr.splice(2,1); 
// ex) [1,2,4,5] index[2]부터 1개만 삭제
```

```js
let a;
a = 1;
a = 2;

// const a = 0;
// const 재대입 불가능 : 선언과 대입을 동시에

// let, const ,로 동시선언 가능
// let one = 1, two = 2, nothing;
// const three = 3, four = 4;

//식별자는 객체에 ''없이 사용할 수 있음 : 식별자의 조건이 아닌 경우 ''을 써서 사용가능
const obj = {
  a : 1,
  '7seven' : 2
}
//식별자 규칙! 꼭 알아두기
// typeof도 연산자임. 이 연산자는 [+,-등등]보다 높은 우선순위 => 그래서 먼저 계산되는 부분에 ()를 적기
```





- number 타입
```js
0x4d === 77; //true
0x4d !== 77; //false
```

- .isInteger()
```js
Number.isInteger(0.2); //이거 정수냐
```

- 연산자
```js
let a = 1;
a++; // 1 증가시키기 전 값을 표현식의 결과값을 반환
++a; // 1 증가시킨 후의 값을 표현식의 결과값으로 반환
let b = a++; //b = 1;
```

- NaN
```js
0.1 + 0.2;
0 / 0; => NaN
parseInt('3'); => 문자열을 숫자열로!
parseInt('asdf') => NaN
```
// NaN인지 아닌지 판별하고싶을때는, 등호를 쓰면 안됨!!!!!!!! => .isNaN()으로 입력
// ===는 숫자비교에만 특화 되어있음. NaN은 숫자가 아니기 때문에 어떤 숫자가 와도 같지 않다.는 규칙이 있음. 즉, NaN은 number타입이지만 number 타입인 NaN과 같지않고, 숫자와도 같지 않다. 그렇기때문에 ===이 붙은건 무조건 같지않음.

// 이렇게 하면 안 됩니다!!!
// if (parsedA === NaN || parsedB === NaN) {
//   alert('숫자를 입력해주세요')
// } else {
//   alert(parsedA + parsedB)
// }

// "NaN은 숫자가 아니기 때문에, 어떤 숫자와도 같지 않다." 는 규칙이 있다.
// => 즉, NaN은 number 타입인 NaN과 같지 않다.
- 이렇게 써야합니다!
```js
if (Number.isNaN(parsedA) || Number.isNaN(parsedB)) {
  alert('숫자를 입력해주세요')
} else {
  alert(parsedA + parsedB)
}
```



- evaluate(평가) : 표현식을 값으로 변환하는 절차
- /object.is() : 실제로 javascript상에서 같은 값인지 비교해서 true, false반환
- .isFinite() 유한한지아닌지 => 무한이 아니면 true => 실행문 출력
```js
const input = prompt('정수를 입력하세요');
const num = parseInt(input);
if (Number.isNaN(num)) {
  alert('정수가 아닙니다.');
} else {
  const result = num * 2;
  alert(`${num}의 두 배는 ${result} 입니다.`);
}
```

- Math
```js
Math 객체
Math.abs(3)
Math.ceil(3.1)
Math.floor(-3.6)
Math.trunc(-3.6)
Math.abs // 절댓값
Math.ceil // 올림
Math.floor // 내림
Math.round // 반올림
Math.trunc // 소수점 아래 잘라내기
Math.max //제일 큰 숫자 반환
Math.min //제일 작은 숫자 반환
Math.max(1,3,6)
Math.random //0과1사이에 아무 실수나 반환
주사위
Math.floor(Math.random() * 6)+1
Math.ceil(Math.random() * 6)

const cards = ['a', 'b', 'c' ]
cards[Math.floor(Math.random() * 3)]

// number 타입의 메소드 => number는 객체가 아니지만, number를 마치 객체인 것처럼 사용할 수 있다. 
```