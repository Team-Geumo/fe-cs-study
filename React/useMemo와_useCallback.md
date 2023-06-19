# useMemo와 useCallback  메소드를 활용해 최적화하는 원리에 대해서 설명하세요.

## 답변

- `useMemo`와 `useCallback`은 성능 최적화를 위해서 사용되는 Hook입니다.
- 이때, `useMemo`는 **특정 결과 값**을 재사용하는 반면에 `useCallback`은 **특정함수를 새로 만들지 않고 재사용**하고 싶을 때 사용합니다.
- 이 둘은 dependency 리스트를 이용하여 그 중 하나가 변경되면 결과에 대해 변경됩니다.

<br>

# useCallback의 동작원리

## 답변

- `useCallback`은 변수가 선언되어지면 해당 함수가 실행됩니다.
- 그 후에 deps의 변경을 통해 값이 변경되면 새로운 함수를 return하고, 값이 바뀌지 않는다면 기존 함수를 return 합니다.

---

## 1. Memoization

- **기존에 수행한 연산의 결과값을 어딘가에 저장해두고 동일한 입력이 들어오면 재활용**하는 프로그래밍 기법
- 적절하게 활용하면 **중복 연산**을 피할 수 있기 때문에 메모리를 조금 더 쓰더라도 애플리케이션의 성능 촤적화 가능

<br>
## 2. useMemo

```javascript
useMemo(() => fn, [deps])
```

- memoization된 **값을 반환**하는 함수
- `deps`로 지정한 값이 변하게 된다면 `() => fn` 함수를 실행하고, 그 함수의 **반환 값을 반환**
    - `deps`: dependency의 약어, 의존성을 뜻하며 `useMemo`가 이 `deps`에 의존하고 있다는 것을 말함

- 예시
    
    ```javascript
    import React, { useState, useCallback, useMemo } from "react";
    
    export default function App() {
      const [ex, setEx] = useState(0);
      const [why, setWhy] = useState(0);
    
      // useMemo 사용하기
      useMemo(() => {console.log(ex)}, [ex]);
    
      // 두 개의 버튼을 설정했다. X버튼만이 ex를 변화시킨다.
      return (
        <>
          <button onClick={() => setEx((curr) => (curr + 1))}>X</button>
          <button onClick={() => setWhy((curr2) => (curr2 + 1))}>Y</button>
        </>
      );
    }
    ```
    
    - 설명
      - X라는 버튼을 클릭했을 때 `setEx`에 의해서 `ex`의 값이 1씩 증가하는데, `ex`의 값이 변하기 때문에 `useMemo`에서 의존성으로 등록한 `ex`가 변화된 것을 감지해 지정한 함수가 실행되고, `console.log`로 인해 `ex` 값이 출력
        
<br>    

### 2.1. useMemo 쓰는 이유

```javascript
import React, { useState, useCallback, useMemo } from "react";

export default function App() {
  const [ex, setEx] = useState(0);
  const [why, setWhy] = useState(0);

  // 버튼 클릭시 ex값이 출력된다.
  console.log(ex); 
  
  return (
    <>
      <button onClick={() => setEx((curr) => (curr + 1))}>X</button>
      <button onClick={() => setWhy((curr2) => (curr2 + 1))}>Y</button>
    </>
  );
}
```

- 컴포넌트의 **state 값이 변하면 리렌더링이 일어남**
    - 위의 코드의 경우, X버튼, Y버튼, 혹은 컴포넌트가 부모 컴포넌트에 의해서 리렌더링될 경우 상태 값에 관계 없이 `console.log`가 찍히는 연산 발생
- 리렌더링이 발생할 경우, **특정 변수가 변할 때에만 `useMemo`에 등록한 함수가 실행되도록 처리하면 불필요한 연산을 하지 않게 됨**
    - 위의 코드의 경우, ex값이 변할 경우에만 연산을 실행할 수 있도록 useMemo를 사용해 ex라는 변수에 의존하도록 등록하는 것

<br>

## 3. useCallback

```javascript
useCallback(fn, [deps])
```

- **메모이제이션된 함수를 반환**
- deps, 의존선이 있는 값이 변하면 fn에 등록한 함수를 반환

<br>

```javascript
useMemo(() => console.log(), [test])
const memoizedCallback = useCallback(() => console.log(), [test])
```

- `useCallback`이 함수를 반환하기 때문에 그 함수를 가지는 **const 변수에 초기화**하는 것이 일반적
- `useMemo`의 경우 deps 값이 변하면 이 함수를 실행해라!라는 느낌으로 활용 가능
- `useCallback`의 사용처
    - 자식 컴포넌트에 props로 함수를 전달하는 경우
    - 외부에서 값을 가져오는 api를 호출하는 경우

<br>

### 3.1. 자식 컴포넌트에 props로 함수를 전달하는 경우

- **함수는 값이 아닌 참조로 비교된다**
    
    ```javascript
    const functionOne = function() {
      return 5;
    };
    const functionTwo = function() {
      return 5;
    };
    // 서로의 참조가 다르기 때문에 false
    console.log(functionOne === functionTwo);
    ```
    
    - 컴포넌트에서 특정 함수를 정의할 경우 각각의 함수들은 모두 고유한 함수가 됨
    - 고유한 함수가 생성될 경우, 부모를 통해 props에 함수를 전달받는 자식 컴포넌트에서는 props가 변경되었다고 판단해 리렌더링 발생

<br>

- `useCallback`을 사용하지 않을 경우
    
    ```javascript
    import React, { useState } from 'react';
    import Profile from './Profile';
    
    function App() {
      const [name, setName] = useState("");
      const onSave = () => {};
    
      return (
        <div className="App">
          <input
            type="text"
            value={name}
            onChange={(e) => setName(e.target.value)}
          />
          <Propfile onSave={onSave} />
        </div>
      );
    }
    ```
    
    - 부모 컴포넌트만 수정하려고 해도 연쇄적으로 하위 컴포넌트들 모두 렌더링 발생
        - name이 변경되어 리렌더링이 발생하면 `onSave`함수가 새로 만들어지고, Profile 컴포넌트의 props로 onSave가 새로 전달
        - Profile 컴포넌트에서 `useMemo`를 사용해도 **이전 onSave와 이후 onSave가 같은 값을 반환하지만 참조가 다른 함수**가 되어버리기 때문에 리렌더링 발생

<br>

- `useCallback` 사용
    
    ```javascript
    import React, { useCallback, useState } from 'react';
    import Profile from './Profile';
    
    function App() {
      const [name, setName] = useState('');
      const onSave = useCallback(() => {
        console.log(name);
      }, [name]);
    
      return (
        <div className="App">
          <input
            type="text"
            value={name}
            onChange={(e) => setName(e.target.value)}
          />
          <Profile onSave={onSave} />
        </div>
      );
    }
    ```
    
    - `onSave` 함수를 재사용하여 자식 컴포넌트의 리렌더링 방지

<br>

### 3.2. 외부에서 값을 가져오는 api를 호출하는 경우

- `useCallback`을 사용하지 않는 경우
    
    ```javascript
    import React, { useState, useEffect } from "react";
    
    function Profile({ userId }) {
      const [user, setUser] = useState(null);
    
      const fetchUser = () =>
        fetch(`https://your-api.com/users/${userId}`)
          .then((response) => response.json())
          .then(({ user }) => user);
    
      useEffect(() => {
        fetchUser().then((user) => setUser(user));
      }, [fetchUser]);
    
      // ...
    }
    ```
    
    - **무한루프** 발생
        - `fetchUser`함수가 변경될 때만 외부에서 api를 가져와 `useEffect`가 실행
        - `Profile` 컴포넌트가 리렌더링이 발생할 경우 `fetchUser` 함수에는 새로운 함수가 할당됨
        - `useEffect` 함수가 호출되어 user 상태값이 바뀌고, state 값이 바뀌었기 때문에 다시 리렌더링

<br>

- `useCallback`을 사용하는 경우
    
    ```jsx
    import React, { useState, useEffect } from "react";
    
    function Profile({ userId }) {
      const [user, setUser] = useState(null);
    
      const fetchUser = useCallback(
        () =>
          fetch(`https://your-api.com/users/${userId}`)
            .then((response) => response.json())
            .then(({ user }) => user),
        [userId]
      );
    
      useEffect(() => {
        fetchUser().then((user) => setUser(user));
      }, [fetchUser]);
    
      // ...
    }
    ```
    
    - `fetchUser` 함수의 참조값을 동일하게 유지
    - api의 옵션으로 사용되는 `userId`가 변동될 때만 `fetchUser`에 새로운 함수가 할당되도록 설정하고, 그것이 아니면 동일한 함수가 실행되어서 무한루프 빠지지 X