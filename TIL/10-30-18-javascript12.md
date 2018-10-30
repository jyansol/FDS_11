# Express
# JavaScript
## 생성자
- 클래스는 함수로 호출될 수 없습니다.
- 클래스 선언은 let과 const처럼 블록 스코프에 선언되며, 호이스팅(hoisting)이 일어나지 않습니다.
- 클래스의 메소드 안에서 super 키워드를 사용할 수 있습니다.
```js
class Person {}
Person() //에러
new Person() //반드시 new를 써야함

function Student(name){
  this.name = 'haha'
}
//window.name이 바뀜.
```
- function 으로 정의한 함수는 var 변수와 비슷하게 작동
## 메소드 정의하기
- getter / setter 속성에 접근해서 함수 실행
- 정적메소드 : 생성자에 . 찍고 사용함
```js
function Person({name,age}){
    this.name = name;
    this.age = age;
}
Person.prototype.introduce = function(){
  console.log(`안녕하세요, ${this.name}입니다.`)
}
const person1 = new Person({name: '윤아준', age: 19});
const person2 = new Person({name: '신하경', age: 20});

//정적메소드
person1.introduce();
Person.sumAge = function(){
  return people.reduce((acc,person));
}
// 이렇게 써야함
//불 - 편

// 이 메소드는 정적 메소드입니다. 이렇게 쓰면 . 찍고 메소드 처럼 사용가능함
static sumAge(...people) {
    return people.reduce((acc, person) => acc + person.age, 0);
  }
}
//정적메소드
//Array.isArray
//Number.isNaN
Person.sumAge(person1,person2)
```
## 클래스필드
```js
//클래스필드
class Counter {
  static initial = 0; // static class field
  // constructor() {
  //   this.count = Counter.initial;
  // }
  // inc(){
  //   return this.count++;
  // }
  // 와 아래와 같이 쓰는것과 같음
  count = Counter.initial; // class field
  name = "지한솔"
  inc() {
    return this.count++;
  }
}
const c = new Counter()
console.log(c.inc());
//생성자
function Counter(){
  this.count = Counter.initial
}
Counter.initial = 0
Counter.prototype.inc = function(){
  return this.count ++;
}
```
## 클래스 필드와 this
```js
class MyClass {
  a = 1;
  getA = () => {
    return this.a;
  }
  //화살표함수의 this는 인스턴스를 가르킴.


  //   getA () {
  //   return this.a;
  // }
  // function 함수 : 어떻게 호출되느냐에 따라서 결정되기때문에
  // getA() 하면 전역객체를 가르킴.
  
}

new MyClass().getA(); // 1
// getA()를 호출하면 undefined
```
> 메소드의 함수를 넘겨줘야하는 경우 화살표 함수를 사용하는 것이 좋다.