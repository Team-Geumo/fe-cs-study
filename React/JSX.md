# JSX가 무엇인가요?

## 답변

JSX는 자바스크립트 코드를 HTML처럼 표현할 수 있는 React 엘리먼트를 생성하는 언어입니다.

---

## 1. JSX란?

- JavaScript XML의 줄임말로, 자바스크립트의 확장 문법
- 브라우저에서 실행하기 전에 코드가 번들링되는 과정에서 **바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환**됨
- JSX는 자바스크립트의 공식적인 문법이라고 할 수 X
    
    JSX는 React가 처음 도입한 추가적인 문법이므로 JavaScript의 공식적인 표준이 아님
    
    JSX는 React의 특정 케이스에 맞춰 개발되었으며, 모든 JavaScript 개발자에게 필요한 문법이 아님
    
- **자바스크립트에서 HTML을 작성하듯이 비슷하게 작성할 수 있도록 해 주는 것**이 JSX의 가장 큰 장점이자, 이를 사용하는 이유

- HTML
    
    ```html
    <div class="App">
      <h1>Hello, world!</h1>
    </div>
    ```
    
- JavaScript
    
    ```jsx
    const div = document.createElement('div');
    div.className = 'App';
    
    const h1 = document.createElement('h1');
    h1.textContent = 'Hello, world!';
    
    div.appendChild(h1);
    
    document.body.appendChild(div);
    ```
    
- React(JSX)
    
    ```jsx
    import React from 'react';
    
    function App() {
      return (
        <div className="App">
          <h1>Hello, world!</h1>
        </div>
      );
    }
    
    export default App;
    ```
    
<br>

## 2. JSX 문법 규칙

### 2.1. 하나의 부모 요소로 감싸야 한다

```jsx
// 잘못된 코드

function App(){
  return(
      <h1>테스트1</h1>
      <h2>테스트2</h2>
  )
}
```

- 올바른 코드
    
    ```jsx
    function App() {
      return (
        <div>
          <h1>테스트1</h1>
          <h2>테스트2</h2>
        </div>
      );
    }
    ```
    
    ```jsx
    // div요소를 사용하고 싶지 않을 때 Fragment라는 기능 사용
    // 코드 상단 import 구문에서 react 모듈에 들어있는 Fragment라는 컴포넌트를 추가로 불러오기
    import React, { Fragment } from "react";
    
    function App() {
      return (
        <Fragment>
          <h1>Hello</h1>
          <h2>Is it working well?</h2>
        </Fragment>
      );
    }
    ```
    
    ```jsx
    // Fragment는 다음과 같은 형태로도 표현할 수 있다.
    function App() {
      return (
        <>
          <h1>Hello</h1>
          <h2>Is it working well?</h2>
        </>
      );
    }
    ```
    
- 하나의 요소로 감싸줘야 하는 이유
    - React에서 사용하는 Virtual DOM 방식에서는 컴포넌트 변화를 감지할 때 효율적으로 비교하고자 **컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 한다**는 규칙이 있기 때문

<br>

### 2.2. 자바스크립트 표현

- JavaScript 값을 JSX 안에서 렌더링 가능
- name의 값을 `{name}`과 같이 넣어서 렌더링 가능
    
    ```jsx
    import React from "react";
    
    function App() {
      const name = "리액트";
      return (
        <>
          <h1>{name}</h1>
          <h2>test</h2>
        </>
      );
    }
    
    export default App;
    ```

<br>

### 2.3. 조건부 연산자

- JSX 내부의 JavaScript 표현식 내에서 if문을 사용할 수 없음
- 조건부 연산자(삼항 연산자) 사용
    
    ```jsx
    function App() {
      const name = "리액트";
      return (
        <div>{name === "리액트" ? <h1>리액트</h1> : <h2>리액트가 아님</h2>}</div>
      );
    }
    ```

<br>

### 2.4. AND 연산자(&&)를 사용한 조건부 렌더링

- 특정 조건을 만족할 때 내용을 보여주고, 만족하지 않을 때 아예 아무것도 렌더링하지 않아야 하는 상황
- 조건부 연산자(삼항 연산자)로도 구현할 수 있지만 AND 연산자를 이용하면 더 짧은 코드로 똑같은 작업 가능
    
    ```jsx
    import React from "react";
    
    function App() {
      const name = "rreact";
      return <div>{name === "react" && <h1>It's correct</h1>}</div>;
    }
    
    export default App;
    
    // 코드 실행하면 브라우저에 아무것도 나타나지 X
    ```
    
- && 연산자로 조건부 렌더링 가능한 이유
    - React에서 false를 렌더링할 때는 null과 마찬가지로 아무것도 나타나지 않기 때문

<br>

### 2.5. undefined 렌더링하지 않기

- React 컴포넌트에서는 함수에서 `undefined`만 반환하여 렌더링하는 상황 만들면 안 됨
    
    ```jsx
    import React from "react";
    import "./App.css";
    
    function App() {
      const name = "undefined";
      return name;
    }
    
    export default App;
    ```
    
    ```bash
    App(...): Nothing was returned from render. This usually means a return statement is missing. 
    Or, to render nothing, return null
    ```
    
- **OR 연산자**를 사용해 방지 가능
    
    ```jsx
    import React from "react";
    import "./App.css";
    
    function App() {
      const name = "undefined";
      return name || "값이 undefined입니다.";
    }
    
    export default App;
    ```
    
- JSX 내부에서 `undefined` 렌더링하는 것은 에러가 나지 않음
    
    ```jsx
    import React from "react";
    import "./App.css";
    
    function App() {
      const name = "undefined";
      return <div>{name}</div>;
    }
    
    export default App;
    ```
