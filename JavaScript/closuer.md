### 클로저란?

클로저는 자바스크립트 뿐만 아니라 함수를 일급객체로 취급하는 함수형 프로그래밍 언어에서 많이 쓰이는 특성이다.

일반적으로 어떤 함수가 자신의 내부가 아닌 외부에서 선언된 변수에 접근하는 것을 뜻함

```
function convertUsdToKrw(dollar) {
  const rate = 1113.5;
  return dollar * rate;
}
```

이 코드는 내부에서 모두 정의가 되었다.

```
const rate = 1113.5;

function convertUsdToKrw(dollar) {
  return dollar * rate;
}
```

이렇게 작성하여도 동일한 결과를 반환한다.

`JavaScript`에서 함수는 매개 변수와 로컬 변수 뿐만 아니라 외부에서 선언된 변수도 자유롭게 접근을 할 수 있다.
이렇게 함수가 자신의 밖에서 선언된 변수에 접근하는 것을 `클로저`라고 한다.

### 예시

```
function batchConvertUsdToKrw(dollars) {
  const rate = 1113.5;
  const convertUsdToKrw = (dollar) => dollar * rate;
  return dollars.map(convertUsdToKrw);
}
> batchConvertUsdToKrw([1, 2, 10, 20, 50, 100])
[ 1113.5, 2227, 11135, 22270, 55675, 111350 ]
```

JS의 배열을 `map()`메서드의 인자로 `convertUsdToKrw`함수가 넘어가고 있다.
`batchConvertUseToKrw()`함수의 내부에서 선언된 `rate`변수는 `convertUsdToKrw`입장에서 보면 외부에서 선언된 것이다.
즉 `convertUsdToKrw()`함수는 클로저이다.

### 장점은 무엇인가?

```
function signUp(username, password, email, phone) {
  const createUser = () => {
    console.log(`${username}과 ${password}를 검증 중...`);
    console.log(`사용자 생성 중...`);
    // DB에 사용자 레코드 저장하는 코드
  };

  const sendNotifications = () => {
    console.log(`${email}로 이메일 전송 중...`);
    console.log(`${phone}로 문자 전송 중...`);
    // 실제로 알람을 전송하는 코드
  };

  createUser();
  sendNotifications();
  console.log("메인 페이지로 이동...");
}
```

`createUser()`함수와 `sendNotifications()`함수에 인자를 담아 보내지 않아도 된다.

```
const add = (function() {
  let num = 0;
//클로저 활용
  return function() {
    // num 을 1 만큼 증가시킨다
    return ++num;
  }
}())

console.log(add())
console.log(add())
console.log(add())
```

add라는 함수 안에 num 변수를 입력해주고, 해당 함수가 상위 함수 add 안에서 선언이 되게 함으로써 해당 함수가 num 값의 상태를 유지하게 하여 활용을 할 수 있다.

```
> signUp("user", "1234", "test@test.com", "123-456-7890", "대한민국")
user과 1234를 검증 중...
사용자 생성 중...
test@test.com로 이메일 전송 중...
123-456-7890로 문자 전송 중...
메인 페이지로 이동...
```

`signUp()` 함수는 4개의 매개 변수를 받는데, `createUser()`함수와 `sendNotifications()`함수 입장에서 보면 모두 외부에서 선언된 변수들이다.

다시 말해, `signUp()` 함수 내부에 2개의 클로저가 있는 것이다.

### 부작용은?

과용하거나 오용하게 되면 오히려 코드 품질 측면에서 부정적인 영향을 미칠 수 있다. 클로저가 많아지게 되면 코드가 읽거나 고치기 어려워지고, 버그가 발생하기 쉬워지기 때문
