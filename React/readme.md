# React 면접 대비

## 💡 질문 목록

#### [✅ React의 개념과 장점, 그리고 컴포넌트란 무엇인가요?](./React의_개념과_장점_및_컴포넌트란.md)
#### [✅ virtual DOM이 무엇인가요? virtual DOM이 좋은 이유에 대해서 설명하세요.](./Virtual_DOM.md)
#### [✅ React에 있는 라이프사이클과 각 라이프사이클의 역할을 설명하세요.](./React%EC%9D%98_LifeCycle.md)
#### ✅ [React Hooks의 장점은 무엇인가요?](./React_Hook_%EC%9E%A5%EC%A0%90.md)
#### ✅ [Class Component와 Function Component의 차이점에 대해서 설명하세요.](./Class_Component_vs_Function_Component.md)
#### ✅ [state를 직접 변경하지 않고 setState를 사용하는 이유에 대해서 설명하세요.](./setState_사용하는_이유.md)
#### ✅ [Props Drilling이란 무엇인가요?](./Props_Drilling.md)
#### ✅ [useMemo와 useCallback  메소드를 활용해 최적화하는 원리에 대해서 설명하세요.](./useMemo와_useCallback.md)
#### ✅ [useCallback의 동작원리](./useMemo와_useCallback.md)
#### ✅ [React에서 상태 변화가 생겼을 때, 변화를 어떻게 알아채는지에 대해서 설명하세요.](./불변성.md)
#### ✅ [JSX가 무엇인가요?](./JSX.md)
#### ✅ [여러가지 상태 관리 라이브러리(Apollo, Redux, MobX 등)의 차이점에 대해서 설명하세요.](./React_상태관리.md)
#### ⬜ React의 내부 작동 원리를 재조정 (Reconciliation) 개념과 함께 설명하세요.
#### ⬜ Class component의 생명주기 메소드에 대해서 설명하세요.
#### ⬜ React router 같은 Client Side Routing에 대해서 설명하세요.
#### ⬜ useEffect 메소드로 componentWillUnmount가 동작할 수 있는 방법에 대해 설명하세요.

<br>


## 💡 질문 답변 정리

#### ✅ React의 개념과 장점, 그리고 컴포넌트란 무엇인가요?
- React는 UI 구축을 위한 자바스크립트 프론트엔드 라이브러리 입니다. 주로 Single Page Application을 만들 때 사용됩니다.
- React의 장점에는 virtual DOM을 사용해서 어플리케이션의 성능을 향상시키고, 클라이언트 사이드 렌더링이 가능합니다. 또한 다른 프레임워크와도 사용이 가능하며, 컴포넌트의 가독성을 높이며 유지보수가 쉽습니다.
- 여기서 컴포넌트란, 레고 블록과 같이 작은 단위로 만들어서 그것을 조립하는 것처럼 개발하는 방법입니다.
- 컴포넌트를 사용한다면 캡슐화, 확장성, 결합성, 재사용성과 같은 이점이 있습니다.

#### ✅ virtual DOM이 무엇인가요? virtual DOM이 좋은 이유에 대해서 설명하세요.
- virtual DOM은 실제 DOM 변화를 최소화 시켜주는 역할을 합니다.
- virtual DOM을 사용하는 이유는 효율성 때문입니다. virtual DOM을 활용하면 실제 DOM을 바꾸는 것보다 시간 복잡도가 낮아집니다. 만약, HTML 파일에 20개의 변화가 생기면 과정 역시 20회가 이루어집니다. 하지만 virtual DOM은 변화된 부분만 가려내어 실제 DOM에 전달하기에 실제 DOM은 1회로 인식하여 단 한번만의 렌더링 과정만 거치게 됩니다.

#### ✅ React에 있는 라이프사이클과 각 라이프사이클의 역할을 설명하세요.
- 리액트의 라이프사이클은 크게 4가지로 설명할 수 있습니다. 최초로 컴포넌트 객체가 생성될 때 한 번 수행되어지는 `componentDidMount()`와 초기에 화면을 그려줄 때와 업데이트가 될 때 호출되는 `render()`가 있습니다. 그리고 컴포넌트의 속성 값 또는 상태값이 변경되면 호출되어지는 `componentDidUpdate()`와 마지막으로 컴포넌트가 소멸될 때 호출되어지는 `componentWillUnmount()`가 라이프사이클의 역할입니다.

#### ✅ React Hooks의 장점은 무엇인가요?
- Hooks의 장점은 `로직의 재사용이 가능`하고 `관리가 쉽다`는 것입니다. 함수 안에서 다른 함수를 호출하는 것으로 새로운 hook을 만들어 볼 수 있습니다. 기존의 class component는 여러 단계의 상속으로 인해 전반적으로 복잡성과 오류 가능성을 증가시켰습니다. 하지만 function component에 hooks에 도입되면서 class component가 가지고 있는 기능을 모두 사용할 수 있음은 물론이고 기존 class component 복잡성, 재사용성의 단점들까지 해결됩니다.

#### ✅ Class Component와 Function Component의 차이점에 대해서 설명하세요.
- class Component는 `여러 단계의 상속`으로 이루어져 있습니다. 그리하여 `복잡성과 오류 가능성을 증가` 시켰습니다. 이로 인해 Function Component가 탄생하게 되었고, class component는 라이프 사이클을 가지며 이로인해 각각 생명주기 메소드에 대해 알고 있어야 합니다. 하지만 function component는 이러한 기능을 `hook을 사용`하여 생명주기에 원하는 동작을 하게 합니다.

#### ✅ state를 직접 변경하지 않고 setState를 사용하는 이유에 대해서 설명하세요.
- `state는 불변성을 유지해야하기 때문`입니다. 컴포넌트는 setState를 비교해서 업데이트가 필요한 경우에만 render함수를 호출하는데 state를 직접 수정하게 되면 리액트가 render함수를 호출하지 않아 상태 변경이 일어나도 렌더링이 일어나지 않을 수 있습니다.

#### ✅ Props Drilling이란 무엇인가요?
- `React의 컴포넌트 트리에서 데이터를 전달하기 위해서 필요한 과정`을 의미합니다. 예를 들어 우리가 App.js에서 데이터를 하위 컴포넌트까지 쭉 전달하려면 데이터가 변경되었을 때 일일히 고쳐야하는 불편함이 있습니다. 이를 해결하기 위해 `전역 상태 관리 라이브러리`인 Recoil, Redux 등을 이용하여 해당 값이 필요한 컴포넌트에게 직접 불러서 사용하는 해결방안이 있습니다.

#### ✅ useMemo와 useCallback  메소드를 활용해 최적화하는 원리에 대해서 설명하세요.
- `useMemo`와 `useCallback`은 성능 최적화를 위해서 사용되는 Hook입니다. 이때, `useMemo`는 **특정 결과 값**을 재사용하는 반면에 `useCallback`은 **특정함수를 새로 만들지 않고 재사용**하고 싶을 때 사용합니다. 이 둘은 dependency 리스트를 이용하여 그 중 하나가 변경되면 결과에 대해 변경됩니다.

#### ✅ useCallback의 동작원리
- `useCallback`은 변수가 선언되어지면 해당 함수가 실행됩니다. 그 후에 deps의 변경을 통해 값이 변경되면 새로운 함수를 return하고, 값이 바뀌지 않는다면 기존 함수를 return 합니다.

#### ✅ React에서 상태 변화가 생겼을 때, 변화를 어떻게 알아채는지에 대해서 설명하세요.
- React는 상태를 **불변성**을 띄게 변경합니다. 그로 인해 상태 객체의 주소값이 변경되면 변화가 되었다는 것을 알 수 있습니다.

#### ✅ JSX가 무엇인가요?
JSX는 자바스크립트 코드를 HTML처럼 표현할 수 있는 React 엘리먼트를 생성하는 언어입니다.

#### ✅ 여러가지 상태 관리 라이브러리(Apollo, Redux, MobX 등)의 차이점에 대해서 설명하세요.
Redux와 Recoil은 둘 다 상태관리 라이브러리입니다. Redux는 중앙 집중식 저장소와 액션 기반 아키텍처를 사용하며, 액션을 디스패치하여 상태를 변경합니다. 반면 Recoil은 분산된 상태를 관리하며, 컴포넌트 내에서 직접적으로 상태를 읽고 쓸 수 있습니다. Redux는 기존에 많이 사용되고 널리 알려져 있지만, Recoil은 상대적으로 최근에 소개되었으며, 훨씬 간편하고 유연한 API를 제공합니다.

#### ⬜ React의 내부 작동 원리를 재조정 (Reconciliation) 개념과 함께 설명하세요.
#### ⬜ Class component의 생명주기 메소드에 대해서 설명하세요.
#### ⬜ React router 같은 Client Side Routing에 대해서 설명하세요.
#### ⬜ useEffect 메소드로 componentWillUnmount가 동작할 수 있는 방법에 대해 설명하세요.

