## this란?

this는 객체와 연관이 있다.

예를들어,

```
const a = {name : "종혁"}
```

이라는 객체가 있고, 특정 상황을 만족하면 this.name을 호출하면 "종혁"이 출력되는 것이다.

이 상황에서, 변수 a는 this의 context 객체라고 한다.

this의 동작방식에는 4가지가 있다.

## 1. 기본 바인딩(전역객체)

크롬창에서 개발자 도구를 키고 `console.log(this)`를 하면 window객체가 나오게 된다.

this의 첫번째 동작 방식은, 전역 객체(window)를 context 객체로 갖는 것이다.

```
let a = 20
console.log(this.a)

function doSomething() {
  this.dummy2 = "가을";
  console.log(this); // window 객체
}

console.log(this.dummy1); // undefined
console.log(this.dummy2); // undefined

this.dummy1 = "겨울";

console.log(this.dummy1); // 겨울
console.log(this.dummy2); // undefined

doSomething();

console.log(this.dummy1); // 겨울
console.log(this.dummy2); // 가을
```

전역 스코프에서 정의한 변수들은 전역 객체에 등록된다.

let a = 20은 window.g = 20 과 같고,
this객체에 프로퍼티(dummy1, dummy2)를 등록하는 것은
(`this.dummy1`) 사실상 전역 스코프에서 변수를 선언한 것이다.

## 2. 암시적 바인딩

```
function test() {
  console.log(this.a);
}

var obj = {
  a: 20,
  func1: test,
  func2: function() {
    console.log(this.a);
  }
};

obj.func1(); // 20
obj.func2(); // 20
```

```
var b = 100;

function test() {
  console.log(this.b);
}

let obj = {
  a: 20,
  func1: test,
  func2: function() {
    console.log(this.b);
  }
};

obj.func1(); // undefined
obj.func2(); // undefined

let gFunc1 = obj.func1;
gFunc1(); // 100
```

함수 내에 `this.a`가 `this.b`로 변경되었다.

위의 첫번째 예시에서는 `obj.func1`과 `obj.func2`는 `undefined` 를 출력하는 것이 이해되지만, `gFunc`이 100이 출력된는건 왜일까?

`전역 스코프에서 생성한 변수는 전역 객체에 등록되기 때문`

`let gFunc1`은 `window.gFunc1`과 같고, `gFunc1`에서 `this context`는 다시 전역객체(window)가 되기 때문에, `window.gFunc1()`과 같아지기 때문

```
let b = 100;

function test() {
  console.log(this.b);
}

var obj = {
  a: 20,
  func1: test,
  func2: function() {
    console.log(this.b);
  }
};

obj.func1(); // undefined
obj.func2(); // undefined

this.gFunc1 = obj.func1; // 실상 전역객체에 프로퍼티를 등록한 것과 같다 -> window.gFunc1 = obj.func1과 같다
this.gFunc1(); // 100
```

즉 결과적으로 `this`를 그냥 사용하면 암시적으로 전역 객체에 바인딩 되는 것

## 3. 명시적 바인딩

함수객체는 `call`,`apply`,`bind`메서드를 가지고 있는데,
명시적으로 this를 바꾸는 함수 메서드 삼총사 bind, call, apply를 사용하면 this가 객체를 가리킵니다.
첫번재 인자로 넘겨주는 것이 `this context`가 된다.

```
function test() {
  console.log(this);
}

let obj = { name: "Dawn" };
test.call(obj); // { name: 'Dawn' }
test.call("원시 네이티브 자료들은 wrapping 됩니다"); // [String: '원시 네이티브 자료들은 wrapping 됩니다']
```

## 4. new 바인딩

```
function MyFn() {
  this.title = 'Hello World!';
  return this;
}
// new 연산자를 이용해서 새로운 객체를 얻는다.
const myfn = new MyFn();
myfn // MyFn {title: 'Hello World!'}
```

## 5. 우선순위

new 바인딩 >= 명시적 바인딩 >>>>>> 넘사벽 >>>>>> 암시적 바인딩 >= 기본 바인딩

## 6. 그런데,, arrow function

- function 키워드로 생성한 일반함수와 화살표 함수의 가장 큰 차이점이 바로 this이다.
- 이를 Lexical this (렉시컬 this)라고 한다.
- 화살표 함수 안에서 this는 언제나 상위 스코프의 this를 가리킨다.
- 일반 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되지 않고, - 함수를 호출 할 때 함수가 어떻게 호출 되는지에 따라 this에 바인딩할 객체가 동적으로 결정된다.
- 화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다.
- 화살표 함수의 this 바인딩 객체 결정 방식은 함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프와 유사하다.
- 화살표 함수는 call, apply, bind 메소드를 사용하여 this를 변경할 수 없다.

```
const fn = {
  title: 'Hello World!',
  tags: [1, 2, 3, 4],
  showTags() {
    this.tags.forEach((tag) => {
      console.log(tag);
      console.log(this); // fn
    });
  }
}
fn.showTags();
```

```
# 실행 결과
1
{title: 'Hello World!', tags: Array(4), showTags: ƒ}
2
{title: 'Hello World!', tags: Array(4), showTags: ƒ}
3
{title: 'Hello World!', tags: Array(4), showTags: ƒ}
4
{title: 'Hello World!', tags: Array(4), showTags: ƒ}

화살표 함수는 자기 바로 위의 객체를 컨텍스트로 참조.
```
