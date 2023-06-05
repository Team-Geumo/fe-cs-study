# Class Component와 Function Component의 차이점에 대해서 설명하세요.

## 답변

- class Component는 `여러 단계의 상속`으로 이루어져 있습니다. 그리하여 복잡성과 오류 가능성을 증가 시켰습니다.
- 이로 인해 Function Component가 탄생하게 되었고, class component는 라이프 사이클을 가지며 이로인해 각각 생명주기 메소드에 대해 알고 있어야 합니다.
- 하지만 function component는 이러한 기능을 `hook`을 사용하여 생명주기에 원하는 동작을 하게 합니다.

---

## 1. Class Component

- React 컴포넌트 선언하는 두 가지 방식 중 하나
- 현재 자주 사용하지 않지만 사용하는 기업들이 있음

<br>

## 2. Class Component vs. Function Component

### 2.1. 일반적 차이

- **Class Component**
  - state, lifeCycle API 사용 가능
  - 메모리 자원을 함수형 컴포넌트보다 조금 더 사용
    - 클래스 인스턴스의 생성과 관리에 필요한 추가적인 오버헤드 때문
  - 임의 메서드 정의 가능
- **Function Component**
  - state, lifeCycle API 사용 불가능 → _Hook을 통해 해결 가능_
  - 메모리 자원을 클래스형 컴포넌트보다 덜 사용
  - 컴포넌트 선언이 편함
  - 빌드한 결과물의 크기 역시 클래스형 컴포넌트보다 작음

<br>

### 2.2. 선언 방식

- **Class Component**

  ```javascript
  import React, { Component } from "react";

  class App extends Component {
    render() {
      const name = "react";
      return <div className="react">{name}</div>;
    }
  }
  ```

  - class 키워드 필요
  - Component를 상속받아야 함
  - render() 메서드 반드시 필요

- **Function Component**

  ```javascript
  import React from "react";
  import "./App.css";

  function App() {
    const name = "react";
    return <div className="react">{name}</div>;
  }

  export default App;
  ```

  - 클래스형 컴포넌트와 비교해서 훨씬 간결하게 코드 작성
  - 함수 자체가 렌더 함수이기 때문에 `render()` 메서드를 사용하지 않아도 됨
  - Component를 상속받지 않아도 됨

<br>

### 2.3. State 사용 차이

- **Class Component**

  - constructor 안에서 `this.state`를 통해 초기 값을 설정 가능
  - constructor 없이도 초기 값 설정 가능
  - 클래스형 컴포넌트의 `state`는 객체 형식

    ```javascript
    constructor(props) {
      super(props);

      this.state = {
        name: "soopiri",
        item: []
      };
    }

    // without constructor
    class App extends Component {
      state = {
        name: "soopiri",
        item: []
      }
    }
    ```

  - `this.setState` 함수로 `state`의 값 변경 가능
    ```javascript
    onClick = {() => {
      this.setState({ price: price+ 100 });
    }}
    ```

- **Function Component**

  - `useState`로 `state` 핸들링
  - `useState` 함수를 호출하면 배열이 반환되는데 첫 번째 원소는 현재 상태
  - 두 번째 원소는 상태를 바꾸어 주는 함수
    ```javascript
    const [message, setMessage] = useState("");
    ```

<br>

### 2.4. Props 사용 차이

- **Class Component**
  - `this.props`로 불러옴
  ```javascript
  class App extends Component {
    render() {
      const { name, age } = this.props;
      return (
        <div>
          안녕? 나는 {name}구, {age}살이야.
        </div>
      );
    }
  }
  ```
- **Function Component**
  - 렌더 함수의 parameter로 props를 전달받아 사용
  ```javascript
  const App = ({ name, age }) => {
    return (
      <div>
        안녕? 난 {name}이구, {age}살이야.
      </div>
    );
  };
  ```

<br>

### 2.5. 이벤트 핸들링

- **Class Component**

  - 함수 선언 시 애러우로 바로 선언이 가능
  - 적용하기 위해 `this` 붙여야 함

  ```javascript
  handleClick = e => {...}

  render() {
    return (
      <>
        <input type="button" onClick={this.handleClick}>버튼</input>
      </>
    )
  }
  ```

- **Function Component**

  - `const` 함수 형태로 선언
  - `this` 필요X

  ```javascript
  const handleClick = () => {...}

  return (
    <>
        <input type="button" onClick={handleClick}>버튼</input>
    </>
  )
  ```

<br>

## 3. 마무리

- 현재는 React 공식 메뉴얼에서도 컴포넌트를 새로 작성할 때 함수형 컴포넌트를 사용하도록 권장하고 있음
- 특히 React 16.8버전부터는 Hook을 지원하며, 함수형 컴포넌트의 단점이던 `state`와 라이프사이클 API의 사용이 불가능하다는 단점 보완
- 하지만 React의 `state`와 생명주기를 이해하기 위한 차원, 유지보수를 진행해야 할 상황이 빈번하게 발생할 수 있다는 점에 있어서 클래스형 컴포넌트의 학습을 등한시해서는 안 될 것 같음..
