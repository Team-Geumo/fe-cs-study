# React Hooks의 장점은 무엇인가요?

## 답변

- Hooks의 장점은 `로직의 재사용이 가능`하고 `관리가 쉽다`는 것입니다.
- 함수 안에서 다른 함수를 호출하는 것으로 새로운 hook을 만들어 볼 수 있습니다. 기존의 class component는 여러 단계의 상속으로 인해 전반적으로 복잡성과 오류 가능성을 증가시켰습니다.
- 하지만 function component에 hooks에 도입되면서 `class component가 가지고 있는 기능을 모두 사용할 수 있음`은 물론이고 `기존 class component 복잡성, 재사용성의 단점들까지 해결`됩니다.

---

## 1. React Hook이란?

- React 클래스형 컴포넌트에서 이용하던 코드를 작성할 필요없이 함수형 컴포넌트에서 다양한 기능을 사용할 수 있게 만들어준 라이브러리
- React 16.8버전에 새로 추가된 기능
- 함수형 컴포넌트에 맞게 만들어진 것으로 함수형 컴포넌트에서만 사용 가능

<br>

## 2. Hook 규칙

### 2.1. 최상위에서만 Hook을 호출해야 한다.

- 반복문이나 조건문 혹은 중첩된 함수 내에서 Hook을 호출하면 안된다.
- React Hook은 호출되는 순서에 의존하기 때문에 조건문이나 반복문 안에서 실행하게 될 경우 해당 부분을 건너뛰는 일이 발생할 수도 있기 때문에 순서가 꼬여 버그가 발생할 수 있다.
- 이 규칙을 따르면 `useState`와 `useEffect`가 여러 번 호출되는 경우에도 Hook의 상태를 올바르게 유지할 수 있다.

<br>

### 2.2. React 함수 내에서만 Hook을 호출해야 한다.

- Hook은 일반적인 js 함수에서는 호출하면 안 된다.
- 함수형 컴포넌트나 custom hook에서는 호출 가능

<br>

## 3. React Hook 장점

### 3.1. 더 빠른 성능과 짧은 코드의 양

- React에서 작성한 코드를 실행할 때 Babel을 이용해서 코드를 컴파일한 후 실행시키는데, 클래스형 컴포넌트일 경우 코드의 양이 길어짐
- 클래스형 컴포넌트에서는 라이프사이클을 이용할 때 `componentDidMount`, `componentDidUpdate`, `componentWillUnmount` 모두 다르게 처리하지만 React Hook을 사용하면 `useEffect` 안에서 모두 처리 가능

```javascript
// class
componentDidMount() {
  this.updateList(this.props.id);
}

componentDidUpdate(prevProps) {
  if (prevProps.id !== this.props.id) {
    this.updateList(this.props.id);
  }
}

updateList = () => {
  feachList(id).then((list) => this.setState({list}));
}

// hooks
useEffect(() => {
  feachList(id).then((res) => setRes(res));
}, [id]);
```

<br>

### 3.2. Wrapper 컴포넌트 양 감소

- HOC 컴포넌트를 Custom React Hooks로 대체하면 Wrapper 컴포넌트를 사용하지 않고도 간단한 구현이 가능
- 공통적으로 적용해야 하는 코드(언어, 테마, 인증 설정 등)가 있는 경우 하단과 같이 감싸서 작성해야 하는데, 이럴 경우 **Wrapper 컴포넌트 양이 엄청나게 증가하고 데이터 흐름을 파악하기 어려워짐**
    
    ```javascript
    <LanguageHOC>
      <ThemeHOC>
        <AuthHOC>
          <MyPage />
        </AuthHOC>
      </ThemeHOC>
    </LanguageHOC>
    ```
    
- hook을 사용하면 데이터를 내려줄 때 어떤 페이지든 감싸지 않아도 됨
    
    ```javascript
    function useAuth() {
      const [users, setSusers] = useState([]);
    
      useEffect(() => {
        fetchUsers().then(users => setUsers(users));
      }, []);
    
      return [users];
    }
    
    function MyPage() {
      const [users] = useAuth();
    
      return (
        <div>
          My Page
          {users.map(({ name, url }) => (
            <div key={name}>
              <h3>{name}, {url}</h3>
            </div>
          ))}
        </div>
      );
    }
    ```
    
<br>

## 4. 용어 정리

### 4.1. Babel

- 최신 JavaScript(ES6 이상)를 이전 버전의 JavaScript(ES5 등)로 변환해주는 컴파일러
- Babel을 사용하면 최신 JavaScript 기능을 사용하여 코드를 작성하면서도, 이전 버전의 JavaScript를 지원하는 브라우저에서도 실행할 수 있게 해줌
- React에서 Babel을 사용하는 목적
    - JSX 문법 변환
    - 최신 JavaScript 기능 지원

<br>

### 4.2. HOC(Higher-order component)

- 고차 컴포넌트
- 화면에 재사용 가능한 로직을 분리하여 컴포넌트로 만들고, 재사용 불가능한 부분(ex: UI)은 파라미터로 받아 처리하는 방법
- 컴포넌트를 받아서 **새로운 컴포넌트**를 반환하는 함수
- 컴포넌트의 props를 조작하거나, 생명주기 메서드를 활용하는 등의 작업을 할 수 있으며, 이를 통해 중복되는 로직을 최소화하고 재사용성을 높이는 데 도움이 됨
- HOC 예시
    
    ```jsx
    function withData(WrappedComponent, selectData) {
      return class extends React.Component {
        constructor(props) {
          super(props);
          this.state = {
            data: selectData(Data, props)
          };
        }
    
        render() {
          // ... and renders the wrapped component with the fresh data!
          // Notice that we pass through any additional props
          return <WrappedComponent data={this.state.data} {...this.props} />;
        }
      };
    }
    ```
    
    - `withData` HOC는 `WrappedComponent`와 `selectData`를 인자로 받아, 새로운 컴포넌트를 반환
    - 새로운 컴포넌트는`selectData`함수를 이용해 특정 데이터를 가져와서 감싸진 컴포넌트에 전달
    - 데이터 선택 로직을 여러 컴포넌트에서 재사용 가능