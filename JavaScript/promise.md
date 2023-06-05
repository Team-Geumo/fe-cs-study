Promise 객체는 JavaScript에서 비동기 작업을 더 편리하게 처리할 수 있도록 도와주는 객체입니다. Promise는 비동기 작업의 최종 완료 또는 실패를 나타내는 값입니다.

Promise는 다음 중 하나의 상태(states)를 가집니다:

1. **대기(pending)**: 초기 상태, 이행되거나 거부되지 않은 상태입니다.
2. **이행(fulfilled)**: 작업이 성공적으로 완료된 상태입니다.
3. **거부(rejected)**: 작업이 실패한 상태입니다.

대기 상태는 이행 상태 또는 거부 상태로 변할 수 있습니다. 하지만 이행 상태와 거부 상태는 다시 대기 상태로 돌아갈 수 없으며, 다른 상태로 변할 수도 없습니다. 이를 불변성(Immutability)이라고 합니다.

Promise 객체는 다음과 같은 방식으로 생성됩니다

```
let promise = new Promise((resolve, reject) => {
  // 비동기 작업을 수행하고,
  // 작업이 성공하면 resolve를 호출하고,
  // 작업이 실패하면 reject를 호출합니다.
});
```

**`then`** 메서드를 사용하면 Promise가 이행 상태가 됐을 때의 처리를 등록할 수 있습니다. **`catch`** 메서드를 사용하면 Promise가 거부 상태가 됐을 때의 처리를 등록할 수 있습니다.

```
promise
  .then(result => {
    // 작업이 성공하면 이 블록이 실행됩니다.
    // result는 resolve 함수에 전달된 값입니다.
  })
  .catch(error => {
    // 작업이 실패하면 이 블록이 실행됩니다.
    // error는 reject 함수에 전달된 값입니다.
  });
```

## 이렇게만 하면 안 와닿죠?

```
let promise = new Promise((resolve, reject) => {
  let success = true; // 이 값이 true라면 resolve를 호출하고, false라면 reject를 호출합니다.
  
  if (success) {
    resolve("성공적으로 완료되었습니다!");
  } else {
    reject("오류가 발생했습니다.");
  }
});

promise
  .then(result => {
    // Promise가 성공적으로 완료되면(즉, resolve가 호출되면) 이 블록이 실행됩니다.
    console.log(result); // "성공적으로 완료되었습니다!"
  })
  .catch(error => {
    // Promise가 실패하면(즉, reject가 호출되면) 이 블록이 실행됩니다.
    console.log(error); // "오류가 발생했습니다."
  });
```

위의 코드에서 **`success`**라는 변수를 true로 설정하면 **`resolve`** 함수가 호출되고 Promise는 fulfilled 상태가 됩니다. 따라서 **`then`** 내부의 코드가 실행되고, 콘솔에 "성공적으로 완료되었습니다!"가 출력됩니다.

반면 **`success`**를 false로 설정하면 **`reject`** 함수가 호출되고 Promise는 rejected 상태가 됩니다. 따라서 **`catch`** 내부의 코드가 실행되고, 콘솔에 "오류가 발생했습니다."가 출력됩니다.

## 그런데 이거 어디서 많이 본 것 같죠?

```
axios.get('https://api.example.com/data')
  .then(response => {
    // 요청이 성공적으로 완료되면 이 블록이 실행됩니다.
    console.log(response.data);
  })
  .catch(error => {
    // 요청이 실패하면 이 블록이 실행됩니다.
    console.log(error);
  });
```

위의 코드에서 **`axios.get`** 메서드는 Promise를 반환하므로 **`then`**과 **`catch`** 메서드를 사용해 성공/실패 시의 처리를 등록할 수 있습니다.

**`then`** 메서드의 콜백 함수에 전달되는 **`response`** 객체는 서버로부터의 응답을 나타냅니다. 이 객체에는 **`data`** 프로퍼티가 있으며, 이 프로퍼티에는 서버로부터 받아온 데이터가 들어 있습니다.

**`catch`** 메서드의 콜백 함수에 전달되는 **`error`** 객체는 에러 정보를 나타냅니다. 이 객체를 통해 에러가 발생했을 때의 상세한 정보를 얻을 수 있습니다.

## 요즘은 try / catch로 합니다.

**`async`** 함수는 항상 Promise를 반환하며, **`await`** 키워드는 Promise가 settled (즉, fulfilled 또는 rejected) 상태가 될 때까지 함수의 실행을 일시적으로 중지시킵니다.

예를 들어, 위에서 본 **`axios.get`** 메서드를 **`async/await`** 문법으로 사용하면 다음과 같이 됩니다

```
async function fetchData() {
  try {
    let response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.log(error);
  }
}

fetchData();
```

위의 코드에서 **`fetchData`**는 **`async`** 함수이므로 이 함수 내부에서 **`await`** 키워드를 사용할 수 있습니다. **`axios.get`** 메서드는 Promise를 반환하므로 **`await`** 키워드를 사용해서 이 Promise가 settled 상태가 될 때까지 기다릴 수 있습니다.

**`await`** 키워드를 사용하면 Promise의 **`then`** 메서드를 사용하는 것보다 비동기 작업의 결과를 더 직접적으로 다룰 수 있습니다. 또한 **`try/catch`** 문을 사용해서 에러를 처리하므로, **`catch`** 메서드를 사용하는 것보다 더 일반적인 에러 처리 방식을 사용할 수 있습니다.