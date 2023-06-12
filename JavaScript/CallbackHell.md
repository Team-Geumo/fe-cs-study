```
loadScript('1.js', function(error, script) {

    if (error) {
      handleError(error);
    } else {
      // ...
      loadScript('2.js', function(error, script) {
        if (error) {
          handleError(error);
        } else {
          // ...
          loadScript('3.js', function(error, script) {
            if (error) {
              handleError(error);
            } else {
              // 모든 스크립트가 로딩된 후, 실행 흐름이 이어집니다. (*)
            }
          });
  
        }
      })
    }
  });
```

## 콜백지옥

위 코드처럼 콜백 함수를 익명함수로 전달하는 과정에서 또 다시 콜백 안에 함수 호출이 반복되어 코드의 들여쓰기 수준이 감당하기 힘들 정도로 깊어지는 현상을 콜백지옥 이라고 합니다.

### 1. ES6에 등장한 Promise로 해결하는 방법
```
loadScript('1.js')
  .then(function(script1) {
    // 스크립트 1 로딩 완료
    return loadScript('2.js');
  })
  .then(function(script2) {
    // 스크립트 2 로딩 완료
    return loadScript('3.js');
  })
  .then(function(script3) {
    // 스크립트 3 로딩 완료
    // 모든 스크립트가 로딩된 후 실행 흐름이 이어집니다.
  })
  .catch(function(error) {
    // 에러 처리
    handleError(error);
  });
```

### 2.  async와 try&catch 로 해결하는 방법

```
async function loadScripts() {
  try {
    var script1 = await loadScript('1.js');
    // 스크립트 1 로딩 완료

    var script2 = await loadScript('2.js');
    // 스크립트 2 로딩 완료

    var script3 = await loadScript('3.js');
    // 스크립트 3 로딩 완료

    // 모든 스크립트가 로딩된 후 실행 흐름이 이어집니다.
  } catch (error) {
    // 에러 처리
    handleError(error);
  }
}
```

### 3. ### 3. 익명함수를 기명함수로 바꾸어서 해결하는 방법

```
function handleScript1(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadScript('2.js', handleScript2);
  }
}

function handleScript2(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadScript('3.js', handleScript3);
  }
}

function handleScript3(error, script) {
  if (error) {
    handleError(error);
  } else {
    // 모든 스크립트가 로딩된 후, 실행 흐름이 이어집니다. (*)
  }
}

loadScript('1.js', handleScript1);
```


