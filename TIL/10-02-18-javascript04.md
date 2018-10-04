# memeo
- 식별자 ( 변수이름, 객체의 속성에도 쓰임 ) / 식별자 규칙
- 원본배열이 변경되지 않는다는게 배열에서 어떤 값을 골라내서 사용할 수 있다!

# 객체 
```js
const name = {
속성 => 속성이름 : 속성 값
}
```
- 'languages': ['Korean', 'English'],
  + '' 를 감싸는 이유 : 식별자 규칙을 만족하는 문자열을 속성이름으로 사용할때는 생략
- 속성 값 부분에 어떤 표현식이 와도 상관없음.
- 다른 변수에 저장된 문자열을 그대로 속성의 이름으로 쓰는 것도 가능
```js
const propName = 'prop';

const obj = {
  [propName]: 1
  // 표현식 [] 의 결과값이 속성 이름
  // 코드 작성 시점에 속성이름을 알지 못하는 경우
};

obj.prop; // 1
```
- 속성 접근법 : 점 표기법, 대괄호 표기법
  + 객체 리터럴을 통해서만 만드는게 아님. 만들어진 뒤에도 추가 가능
  + 방법1 `점 표기법` : person.name = '윤아준'; => 식별자 규칙을 만족하는 경우에만 사용가능 
    그렇지 않은 경우 `.['한국 나이']`(과 똑같은 속성이름을 찾겠다. = 표현식)    
- 속성 이름을 알지 못하는 경우, [] 표기법을 사용해서    
  ```js
  const propName = promt ('속성이름 입력하세요');
  const obj = {}
  obj[propName] = 1
  ```
- delete연산자 : delete person.address; => true, false 반환
- 속성이 객체에 존재 하는지 확인하기
```js
'name' in person; // true
'phoneNumber' in person; // false
```
- 메소드 : 속성접근자를 이용해서 호출, 객체의 속성에 함수를 가지고 있음.
  + `메소드의 this` 라는 keyword 사용가능 : 해당 메소드를 갖고 있는 객체에 접근가능 ( ex: this.name => this === 해당객체 )
```js
const person = {
  greet: function() {
    return 'hello';
  }
  // 축약표기법
  // greet() {
  //   return 'hello';
  // }
};

person.greet(); // 'hello';
```
- 객체 리터럴 안에서 함수, 축약표기법쓸때 `,` 로 구분짓기!

# 생성자 (constructor)
- 대문자로 시작 : 관례! `best practice !`
- 어떤 함수에든 new 를 붙이면 객체가 됨.
- 방법 : 
```js
//객체 생성 기본 문법
const obj = new Object();

//생성자 정의
function Person(name) {
  this.name = name;
}

// 생성자를 통한 객체 생성
const person1 = new Person('윤아준');
```
- 비슷하게 생긴 객체를 생성할때, (ex:게임캐릭터) '객체'를 만들어내는 '함수' => 똑같아야할 부분은 정의해두고, 달라야할 부분만 재정의
- 인스턴스 : 생성자를 통해 생성된 객체 `ex : person1 은 person의 인스턴스다!`
- 메소드를 넣는 방법 : 생성자 안에 넣지 않고 `.prototype`을 이용해서 넣는 방법도 있음. => 스터디에서 지향했던 방법!
  + mdn 검색했을때 메소드 앞에 .prototype 붙어있었던 의미

  # 배열
  - 객체와 달리 순서가 있음.
  - 배열은 Array 생성자의 인스턴스입니다. 그러니까, 배열의 프로토타입으로 Array.prototype 객체가 지정되어 있습니다. => 생성자로부터 생성된 객체구나!
  - Array.of : 인수가 몇개더라도 인수들이 들어있는 배열 vs Array(1) // empty * 1 => 자주 쓰이지 않음
  - `Array.from` : 유사배열객체 ex ) 문자열
  ```js
  Array.from('hello'); // ["h", "e", "l", "l", "o"]
  //'hello'.split('');과 같다.
  ```
  - .fill()
  ```js
const arr = [1, 2, 3, 4, 5];

// 전체를 0으로 채우기
arr.fill(0);
console.log(arr); // [ 0, 0, 0, 0, 0 ];

// 인덱스 2와 4 사이를 1로 채우기
arr.fill(1, 2, 4);
console.log(arr); // [ 0, 0, 1, 1, 0 ];
  ```
- 생성자와 .fill()
```js
new Array(1000); // [empty × 1000]
new Array(1000).fill(5); // [5, 5, 5, 5, ...]
// web보다는 게임이나 이미지편집때 자주 쓰임
```  
- `.push()` 와 `.pop()`
  + 오른쪽에 추가, 제거
  + 이미 만들어진 배열, 빈배열
  + .push('one', 'two'); // 2개 이상도 가능
  + .pop(); // 배열의 맨 끝의 값을 가져와서 반환 + 지움 하는 특징!
  + 비어있는 arr.pop(); // undefined (더 이상 배열에 요소가 남아있지 않으면 `undefined`를 반환)]
- `.unshift()` 와 `.shift()`  
  + 왼쪽에 추가, 제거
  + 배열의 추가/제거된 값을 가져와서 반환 + 지움 하는 특징!
  + ex )
  ```js
  const arr = [];
  arr.unshift(1); // 1 (요소가 추가된 후의 배열의 길이를 반환)
  arr.unshift(2, 3); // 3

  console.log(arr); // [ 2, 3, 1 ]
  ```
- `.splice()`
  + 배열의 어디에서든 추가, 제거  
  + 바꿔치기 한 것을 반환 + 변환 하는 특징!
  + splice(2,0,'ㄱ','ㄴ') => `2 를 틈이라고 생각하면 쉬움` [0ㄱ1ㄱ2ㄱ3ㄱ4ㄱ5]
  + ex)
  ```js
  let arr = [1, 2, 3, 4, 5];

  // 인덱스 `1`인 요소부터 `3`개을 바꿔치기 합니다.
  // `splice` 메소드는 바꿔치기를 통해 제거된 요소들을 반환합니다.
  arr.splice(1, 3, 'two', 'three', 'four'); // [2, 3, 4] //index가 1인것부터 3개를!
  console.log(arr); // [ 1, 'two', 'three', 'four', 5]

  //3개를 하나로 바꾸는 것도 가능
  arr.splice(1, 3, 'three'); // [2, 3, 4]
  //[1, 'three', 5]

  //뒤쪽 인수를 생략하면, 요소를 제거할 뿐 배열에 아무것도 삽입하지 않습니다.
  arr.splice(1, 3); // [2, 3, 4]
  // [1, 5]
```
- .reverse() : ~을 한 원본배열을 반환
- .slice() : ~한 값이 반환 하지만 원본배열을 그대로 유지 => default : .slice(0, arr.length);
  + 원본배열을 그대로 두고 복사해서 편집하고싶다
    ```js
    const arr = [3, 6, 7, 8, 1]
    //arr.sort(); 사용하면 원본 배열이 바뀜
    const newArr = arr.slice();
    newArr.sort()
    //원본배열에 영향을 미치지 않음
    ```
- javascript 교재에 배열 유지 / 바꾸는 메소드 정리 확인!
- `.sort()` : 
  + 반드시 `비교함수`가 필요함! 왜냐하면 비교함수 없이 사용하면 요소를 전부 문자열로 변환하기때문에 유니코드 코드포인트 순으로 정렬.
  + 원본 배열 변경!
- `['abc', 'DEF', 'aBC'].sort((x, y) => x.localeCompare(y));` 사전순 정리가능 === 비교함수 쓴 .sort()
- 배열 순회하기
  + for 
  + forEach : `arr.forEach((item, index, array))`
  + for ... of : ES2015 도입 , index가 필요없고 순회하기 위한 목적!
  ```js
  for (let 변수이름 of 배열이름) {
  console.log(변수이름);
  }
  for (const 변수이름 of 배열이름) {
  console.log(변수이름);
  //변수를 매번 새로 만듬. block scope를 갖는다.
  }
```
- `.map()` 
- `.filter()` : 원본배열 변경하지 않고 
- 