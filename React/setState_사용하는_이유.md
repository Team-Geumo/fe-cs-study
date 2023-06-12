# state를 직접 변경하지 않고 setState를 사용하는 이유에 대해서 설명하세요.

## 답변

- state는 불변성을 유지해야하기 때문입니다.
- 컴포넌트는 `setState`를 비교해서 업데이트가 필요한 경우에만 `render`함수를 호출하는데 `state`를 직접 수정하게 되면 리액트가 `render`함수를 호출하지 않아 상태 변경이 일어나도 렌더링이 일어나지 않을 수 있습니다.

---

## 1. state란?

- 간단히 말하면 변수
- 일반 변수와 다르게 값이 변하면 렌더링 발생
    - 값이 변하게 되면 연관있는 컴포넌트들이 다시 렌더링되어 화면이 바뀜
- props와 같이 컴포넌트 렌더링에 영향을 주는 데이터를 갖고 있는 **객체**이고, **컴포넌트 안에서 관리**됨

<br>

## 2. setState란? 필요한 이유는?

> `setState(updater, [callback])`
콜백 함수가 실행된 후 리렌더링됨
> 
- state를 변경할 때 사용하는 함수
- 컴포넌트는 현재 this.state와 setState를 비교해서 업데이트가 필요한 경우에만 render 함수를 호출
    - state를 직접 수정하게 되면 리액트가 render 함수를 호출하지 않아 상태 변경이 일어나도 렌더링이 일어나지 않을 수 있음
- 예시 코드
    
    ```javascript
    // 클래스형
    class Example extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          count: 0
        };
      }
    
      render() {
        return (
          <div>
            <p>You clicked {this.state.count} times</p>
            <button onClick={() => this.setState({ count: this.state.count + 1 })}>
              Click me
            </button>
          </div>
        );
      }
    }
    
    // 함수형
    function Example() {
      // 새로운 state 변수를 선언하고, count라 부르겠습니다.
      const [count, setCount] = useState(0);
    
      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => setCount(count + 1)}>
            Click me
          </button>
        </div>
      );
    }
    ```

<br>

## 3. setState의 동작

- setState는 **비동기적**으로 동작
- 예시 코드
    
    ```jsx
    function App() {
      const [state, setState] = useState(1);
    
      const onClick = () => {
        setState(state + 1);
        console.log(state);
      };
    
      return (
        <div className="App">
          <button onClick={onClick}>+1</button>
          <p>현재 값 {state}</p>
        </div>
      );
    }
    ```
    
    - 결과
        - 버튼을 클릭하면 `onClick` 함수가 호출되고, `setState` 함수를 통해 `state` 값이 1씩 증가
        - `console.log(state)` 실행되고, `state` 값은 업데이트 전의 값인 1이 출력
    - 이유
        - `setState` 함수는 비동기적으로 상태를 업데이트 하기 때문
        - `setState` 함수는 상태를 업데이트하고 컴포넌트를 다시 렌더링하지만, 업데이트된 상태를 즉시 반영하지 않음
        - 따라서 `console.log`가 실행될 때는 업데이트 전의 상태가 출력됨
    - 결론
        - React는 `setState`를 킵해뒀다가 다른 기타 코드들을 처리하고 브라우저 이벤트가 끝날 시점에 state를 일괄적으로 업데이트

<br>

## 4. state 설정은 왜 비동기로 작동하는가?

- state는 값이 변경되면 리렌더링이 발생
    - 변경되는 state가 많을 경우 리렌더링이 계속 일어날테고 속도가 저하될 것
- 변경된 값들을 모아 한 번에 업데이트를 진행하여 렌더링을 줄이고자 **배치(Batch)** 기능을 사용해 비동기로 작동
    - 배치 업데이트는 16ms 주기