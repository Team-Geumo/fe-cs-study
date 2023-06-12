### 정적 타입 체크:

- JavaScript: JavaScript는 동적 타입 언어로, 변수의 타입을 선언하지 않고 사용할 수 있습니다. 이는 자유로움과 유연성을 제공하지만, 타입 관련 오류를 런타임 시점에만 발견할 수 있습니다.

```jsx
const a : number=1
const b=1

return a+b 
-> 11

위도, 경도 필요한 경우..
 내 위도 = 216.1
 내가 있는 위도 + 0.03 = 2.16113 (동적 사실을 모를 떄 일) 
```

- TypeScript: TypeScript는 정적 타입 언어로, 변수의 타입을 명시적으로 선언하고 타입 검사를 수행합니다. 이는 개발자가 컴파일 단계에서 타입 오류를 발견하여 조기에 수정할 수 있다는 장점이 있습니다.

### 타입 주석과 타입 추론:

- JavaScript: JavaScript에서는 변수에 타입 주석을 명시적으로 추가하지 않습니다. 변수에 할당된 값에 따라 동적으로 타입이 추론됩니다.
- TypeScript: TypeScript에서는 변수에 타입 주석을 추가하여 명시적으로 타입을 지정할 수 있습니다. 또한, 타입 추론 기능을 사용하여 변수의 타입을 자동으로 추론할 수 있습니다.

### 인터페이스와 타입 추론:

- JavaScript: JavaScript에는 인터페이스 개념이 없습니다. 객체의 형태를 설명하기 위해 주로 주석이나 문서화를 사용합니다.
- TypeScript: TypeScript에서는 인터페이스를 사용하여 객체의 형태를 정의할 수 있습니다. 이는 코드의 가독성을 높이고, 타입 체크 및 타입 추론에 활용됩니다.

---

### 코드 컴파일:

- JavaScript: JavaScript 코드는 브라우저나 Node.js와 같은 JavaScript 엔진에서 직접 실행됩니다. 따로 컴파일 과정이 필요하지 않습니다.
- TypeScript: TypeScript 코드는 JavaScript 코드로 변환되기 전에 컴파일되어야 합니다. TypeScript 컴파일러를 사용하여 TypeScript 코드를 JavaScript 코드로 변환합니다.

---

### ECMAScript 버전 지원:

- JavaScript: JavaScript는 ECMAScript 표준을 따르며, 여러 버전의 ECMAScript를 지원합니다. 하지만, 모든 브라우저에서 모든 기능을 지원하지는 않습니다.
- TypeScript: TypeScript는 ECMAScript 표준을 기반으로 하며, 최신 버전의 JavaScript 문법과 기능을 지원합니다. TypeScript 컴파일러는 지정된 ECMAScript 버전을 대상으로 JavaScript 코드를 변환할 수 있습니다.

### 생태계와 도구 지원:

- JavaScript: JavaScript는 널리 사용되는 언어로, 다양한 라이브러리, 프레임워크, 도구, 커뮤니티 등 다양한 생태계와 지원을 가지고 있습니다.
- TypeScript: TypeScript는 JavaScript의 상위 집합이기 때문에 JavaScript 생태계와 호환됩니다. TypeScript는 추가적인 타입 관련 도구와 개발 환경의 지원을 받을 수 있습니다.

JavaScript는 웹 개발에서 가장 널리 사용되는 언어 중 하나이며, TypeScript는 JavaScript의 확장으로 (superset) 정적 타입 체크와 타입 안정성을 강화한 언어입니다. TypeScript는 대규모 프로젝트에서 특히 유용하며, 개발자들이 코드의 유지 보수성과 안정성을 향상시킬 수 있도록 도와줍니다.