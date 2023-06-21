## this의 정의

### this란?

- this란 JavaScript의 예약어다.
- 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-refernece variable)이다.
- this는 자바스크립트 엔진에 의해 암묵적으로 생성된다.
- this는 코드 어디서든 참조할 수 있지만, 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수 이므로 일반적으로 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미가 있다.

### this의 동작 과정

- 함수를 호출하면 인자와 this가 암묵적으로 함수 내부에 전달된다.
- 함수 내부에서 인자를 지역 변수처럼 사용할 수 있는 것처럼, this도 지역 변수처럼 사용할 수 있다.
- 그러나 this가 가리키는 값, this의 바인딩은 함수 호출 방식에 의해 동적(유기적)으로 결정된다.

### 바인딩?

- 식별자와 값을 연결하는 과정
- 변수선언은 변수 이름과 확보된 메모리 공간의 주소를 바인딩 하는 것
- this바인딩은 this와 this가 가리킬 객체를 바인딩 하는 것

# 1. this를 전역에서 사용한 경우

- 브라우저의 경우에 this는 항상 window라는 전역 객체를 참조
- 전역 객체란 전역 범위에 항상 존재하는 객체를 의미한다.
- 브라우저 안에서 모든 변수, 함수는 window라는 객체의 프로퍼티와 메소드

```jsx
a = 'a'
-> "a"
this.a
-> "a"
window.a
-> "a"
```

# 2. this를 함수 내부에서 사용한 경우

- 함수는 전역에서 선언된 일반 함수와 객체 안의 메소드로 크게 구분 가능
- 객체 안에 선언된 함수를 전역에 선언된 함수가 구분하기 위해 메소드라고 한다.
- 즉, this는 함수 내부에서 호출하는 방법에 의해 바뀐다.
- 엄격모드(strict mode)에 따라 참조 값이 달라지는데, 이 때 this는 undefined가 바인딩 된다.

# 사용해보러 가즈아

## 1. 전역에 선언된 함수에서 this

### Case 1.

- 함수가 전역에 선언되어 있는 경우

```jsx
function Kim(){
	return this;
}
Kim(); // window 객체 출력
```

### Case 2.

- new 연산자를 사용해서 생성자 함수 방식으로 인스턴스를 생성한 경우

```jsx
function Hello() {
  this.title = 'Hello World!';
  return this;
}
// new 연산자를 이용해서 새로운 객체를 얻는다.
const hello = new Hello();
-> hello // Hello {title: 'Hello World!'}
```

- JavaScript에서 생성자 함수는 새로운 객체를 생성하고 초기화하는 역할을 합니다.
- 생성자 함수 `Hello` 는 빈 객체를 만들고, 이 생성자 함수는 **`this.title = 'Hello World!'`**라는 코드를 포함하고 있는데, 여기서 **`this`**는 함수가 실행되는 컨텍스트(즉, 해당 함수를 호출하는 객체)를 가리킵니다.
- **`new`** 연산자를 사용하여 `hello`의 새 인스턴스를 만듭니다. **`new`** 연산자는 새 객체를 생성하고 그 객체를 **`this`**에 바인딩한 후에 `Hello` 생성자 함수를 호출합니다. 이렇게 호출된 함수에서 **`this`**는 새로 생성된 객체를 가리킵니다.
- 따라서 `Hello` 객체는 `Hello` 함수를 통해 생성되었으며, **`title`** 속성이 'Hello World!'로 초기화되었습니다.

## 2. 객체의 메소드 함수에서 this

```jsx
const obj = {
  name: 'Example Object',
  printName: function() {
    console.log(this.name);
  }
};

obj.printName(); // 'Example Object'
```

## 3. call, apply, bind

- JavaScript는 **`call`**, **`apply`**, **`bind`**와 같은 메서드를 제공하여 함수 또는 메서드의 **`this`**값을 명시적으로 설정할 수 있습니다. 이러한 메서드를 사용하면, 함수의 **`this`** 값을 원하는 객체로 설정할 수 있습니다.

```jsx
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const obj1 = { name: 'Alice' };
const obj2 = { name: 'Bob' };

// Using call
greet.call(obj1, 'Hello', '!'); // 'Hello, Alice!'
greet.call(obj2, 'Hi', '...'); // 'Hi, Bob...'

// Using apply
greet.apply(obj1, ['Hello', '!']); // 'Hello, Alice!'
greet.apply(obj2, ['Hi', '...']); // 'Hi, Bob...'

// Using bind
const boundGreet1 = greet.bind(obj1);
const boundGreet2 = greet.bind(obj2);

boundGreet1('Hello', '!'); // 'Hello, Alice!'
boundGreet2('Hi', '...'); // 'Hi, Bob...'
```

- **`call`**은 함수를 호출하면서 첫 번째 인자로 **`this`** 값을 설정하고, 이후 인자들을 함수에게 직접 전달합니다.
- **`apply`**는 **`call`**과 동일하게 첫 번째 인자로 **`this`** 값을 설정하지만, 이후 인자들을 배열로 전달합니다.
- **`bind`**는 함수를 호출하지 않고, 대신 새로운 함수를 생성합니다. 이 새 함수는 **`this`** 값이 원래 함수에게 **`bind`**의 첫 번째 인자로 설정된 상태로 호출됩니다. 이후 인자들은 새로 생성된 함수를 호출할 때 전달됩니다.
- 이러한 메서드들은 **`this`** 바인딩이 동적으로 결정되는 JavaScript에서 함수와 객체 사이의 관계를 편리하게 조작하게 해줍니다.

## 4. 화살표 함수에서의 this

- 화살표 함수(**`arrow function`**)는 일반 함수와 달리 자신만의 **`this`** 바인딩을 생성하지 않습니다. 대신, 화살표 함수는 **`this`** 값을 자신을 둘러싼 상위 스코프에서 가져옵니다(`lexical this`). 이 특성 덕분에, 특정 콜백 내에서 외부 스코프의 **`this`**에 접근하고 싶을 때 유용하게 사용할 수 있습니다.

```jsx
const obj = {
  value: 'Hello World',
  printValue: function() {
    setTimeout(function() {
      console.log(this.value); // undefined
    }, 1000);
  }
};

obj.printValue();
```

이 경우 **`setTimeout`** 내의 함수에서 **`this`**는 **`window`** (브라우저 환경에서) 또는 **`global`** (Node.js 환경에서)를 가리킵니다. 왜냐하면 **`setTimeout`** 내부의 콜백 함수는 일반 함수이기 때문에, 그 함수의 **`this`**는 기본적으로 전역 객체를 가리키게 됩니다.

### 그런데 이런 문제를 해결하기 위해 화살표 함수를 사용할 수 있습니다.

```jsx
const obj = {
  value: 'Hello World',
  printValue: function() {
    setTimeout(() => {
      console.log(this.value); // 'Hello World'
    }, 1000);
  }
};

obj.printValue();
```

- 위의 코드에서 **`setTimeout`** 내부의 함수는 화살표 함수입니다. 화살표 함수는 자신만의 **`this`** 바인딩을 생성하지 않으므로, **`this.value`**가 **`obj.value`**를 참조합니다. 따라서 이 경우, **`this`**는 **`obj`**를 가리키게 됩니다. 이것이 화살표 함수에서의 **`this`** 바인딩이 lexical(즉, 정적)하다는 것을 보여주는 예입니다.