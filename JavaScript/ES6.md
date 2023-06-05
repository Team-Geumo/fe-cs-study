## JavaScript의 탄생

- 1994년 당시 넷스케이프 커뮤니케이션스사의 Netscape Navigator(NN) 브라우저가 전 세계 점유율을 80% 이상 독점하며 브라우저의 표준 역할을 함
- 당시 넷스케이프에서 재직 중이던 브랜던 아이크가 HTML을 동적으로 동작하기 위한 회사 내부 프로젝트를 진행 중 JS를 개발
- JavaScript 이름의 변천사
    - Mocha -> LiveScript -> JavaScript(1995)
- 그러나 1995년 경쟁사 마이크로소프트에서 이를 채택하여 커스터마이징 한 JScript를 만듦
- 이를, IE 1.0에 탑재 - > 1차 브라우저 전쟁의 시작

### 제 1차 브라우저 전쟁

- 넷스케이프 vs 마이크로소프트 (이하 MS)
- 빌게이츠 주도하에 MS는 1997년 IE 4를 발표하면서 시장을 장학하기 시작
    - 당시 윈도우 OS의 시장 점유율은 90%
    - 글로벌 기업 MS의 공격적인 마케팅
- MS의 승리로 끝나며 2001년부터 IE의 점유율은 90%를 상회
- 1998년 넷스케이프에서 나온 브랜던 아이크 외 후계자들은 모질라 재단을 설립
    - 파이어폭스를 통해 IE에 대항하며 꾸준히 점유율을 올려나 나감
- MS의 폭발적 성장, IE3에서 자체적은 JScript를 지원, 호환성 문제로 크로스 브라우징 등의 이슈 발생
- 이후 넷스케이프 후계자들은 모잘리 재단 기반의 파이어폭스를 개발

### 제 2차 브라우저 전쟁

- MS vs Google
- 2008년 Google의 Chrome(이하 크롬) 브라우저 발표
- 2011년 3년만에 파이어폭스의 점유율을 돌파 후 2012년 전 세계 점유율 1위 등록
- 크롬의 승리 요인
    - 압도적인 속도
    - 강력한 개발자 도구 제공
    - 웹 표준

### 파편화와 표준화

자바스크립트는 넷스케이프에서 개발하였습니다. 그리고 그에 대항하기 위해 MS에서는 J스크립트를 만들었음. 

이처럼 브라우저 마다 스크립트 언어가 다르게 때문에 서로 호환이 되지 않고 **파편화**가 생기기 시작했습니다. 파편화는 간단히 말해서 똑같은 코드인데 어떤 브라우저에서는 제대로 실행되고 어떤 브라우저에서는 에러가는 현상을 의미합니다.

**이런 파편화를 막으려면 표준을 만드는 것이 중요합니다.** 그래서 넷스케이프는 96년 11월에 브라우저에서 돌아가는 스크립트 언어를 표준화하기 위해서 Ecma 인터네셔널이라는 국제 표준화 기구에 자바스크립트 기술 규격 제정을 요청합니다.

Ecma 인터네셔널이라는 곳은 C++, C#, CLI, 파일구조, JSON 등 다양한 표준을 제정하는 기구입니다. 과거에는 ECMA(European Computer Manufatures Association)이라는 유럽 컴퓨터 제조 협회였지만 지금은 Ecma 인터네셔널로 이름을 바꿔 유럽 뿐 만 아니라 전 세계적인 표준화 작업을 하는 국제 표준화 기구입니다.

### JavaScript ES6+

### 1) ES1 ~ ES3 (1997~1999년)

97년 ES1을 시작으로 98년 ES2, 99년 ES3가 발표되었습니다. ES3에서는 try/catch 문법이 들어갔습니다.

### 2) ES4 (폐기)

이 후 ES4 표준 작업이 진행되었지만 언어에 얽힌 정치적인 견해 차이로 ES4 명세는 폐기되었습니다.

### 3) 2015년 ES2015(ES6) 탄생

- ES6는 ECMAScript 2015라고도 합니다. ES6에서는 class, module 등이 적용되었고, 콜백 지옥을 해결할 Promise와 함수형 프로그래밍 및 Typescript의 기능이 문법적으로 흡수되기도 하였다.
- 이때부터 버전 순서가 아닌 출시 연도를 붙이는 것이 공식 명칭이나 통상적으로 ES6라 부른다.
- 주요 문법
    
    ### **1. const & let**
    
    const와 let은 변수 선언을 위한 키워드입니다. (기존엔 var로 변수 선언)
    
    - const : var보다 강력하며, 변수가 사용되면 다시 할당할 수 없습니다. (상수이므로 변경 불가)
    
    * 아래 코드처럼 변경 불가능
    
    ```
    const hobby = "walking";
    hobby = "exercise";// Error
    ```
    
    ---
    
    - let : const와 달리 새로운 값을 가질 수도 있고 재할당도 가능합니다. (변경 가능)
    
    ```
    let phone = "iphone11";
    phone = "iphone13";
    console.log(phone);// Result : iphone13
    ```
    
    ---
    
    ### **2. Arrow Function**
    
    Arrow Function은 코드가 간결해져서 가독성이 높아지는 함수 문법입니다.
    
    ```
    // ES5 문법var sample = function sample(a, b) {
    	console.log(a, b);
    };
    
    // ES6 문법let sample = (a, b) => {console.log(a,b)};
    ```
    
    ---
    
    - Arrow Function을 map, filter 등 내장 함수에도 사용할 수 있습니다.
    
    ```
    // ES5 문법var testArray = ['a', 'b', 'c', 'd'];
    var arr = testArray.map(function(item) {
    	return item;
    });
    console.log(arr);// Result :  ['a', 'b', 'c', 'd']// ES6 문법let engArray = ['a', 'b', 'c', 'd'];
    let arr2 = engArray.map((item) => item);
    console.log(arr2);// Result :  ['a', 'b', 'c', 'd']
    ```
    
    ---
    
    ### **3. Template Literals**
    
    기존 ES5 문법에서는 문자열을 연결하기 위해 더하기(+) 연산자를 사용했는데, ES6에서는 더하기(+) 연산자를 사용하지 않고 문자열 내에서 변수로 사용이 가능합니다.
    
    *** ES5 작은따옴표(')와 ES6 백틱(`)을 헷갈리지 않도록 주의 !**
    
    ```
    // ES5 문법function myFunc1(name, age) {
    	return name + '는 ' + age + '살';
    }
    console.log(myFunc1('도리', 24));// Result : 도리는 24살// ES6 문법const myFunc2 = (name, age) => {
    	return `${name}는 ${age}살`;
    };
    console.log(myFunc2('도리', 24));// Result : 도리는 24살
    ```
    
    ---
    
    ### **4. Default Parameters (기본 매개 변수)**
    
    ```
    //ES5 문법const myFunc1 = (name,age) => {
        return `${name}는 ${age}살`;
    };
    console.log(myFunc1('도리'));// Result : 도리는 undefined살
    ```
    
    위 코드를 보면 매개 변수를 정의하지 않는 경우 undefined를 반환하는데 아래 코드처럼 정의하면 변수에 해당 값을 사용할 수 있습니다.
    
    ```
    //ES6 문법const myFunc2 = (name,age = 24) => {
        return `${name}는 ${age}살`;
    };
    console.log(myFunc2('도리'));// Result : 도리는 24살
    ```
    
    ---
    
    ### **5. Array and Object Destructing (배열 및 객체 비구조화)**
    
    배열 및 객체 비구조화를 통해 객체의 값을 새로운 변수에 쉽게 할당할 수 있고, 코드가 간결해집니다.
    
    *** 속성명과 동일하지 않은 변수를 할당하면 undefined가 반환됩니다 !**
    
    ```
    // ES5 문법const myInfo1 = {
        name : '도리',
        age : 24,
        job : 'programmer'
    };
    
    let name = myInfo1.name;
    let age = myInfo1.age;
    let job = myInfo1.job;
    
    console.log(name, age, job);// Result : 도리 24 programmer// ES6 문법const myInfo2 = {
        name : '도리',
        age : 24,
        job : 'programmer'
    };
    
    let { name, age, job } = myInfo2;
    
    console.log(name, age, job);// Result : 도리 24 programmer
    ```
    
    ---
    
    - 변수명을 아래 코드처럼 콜론(:)을 사용하여 바꿀 수 있습니다.
    
    ```
    const myInfo2 = {
        name : '도리',
        age : 24,
        job : 'programmer'
    };
    
    let { name: changeName, age, job } = myInfo2;
    
    console.log(changeName);// Result : 도리
    ```
    
    ---
    
    - 배열인 경우 아래 코드와 같이 작성하면 됩니다.
    
    ```
    const arr = ['집', '회사', '카페'];
    let [place1, place2, place3] = arr;
    
    console.log(place1, place2, place3);// Result : 집 회사 카페
    ```
    
    ---
    
    ### **6. Promise - 추후 더 자세히**
    
    Promise는 비동기 코드인데, 주로 API에서 데이터를 가져오는 등 시간이 걸리는 함수를 가지고 있을 때 사용합니다.
    
    ```
    const promiseFunc = () => {
        return new Promise((resolve, reject) => {
            resolve("success!");
        });
    };
    
    console.log(promiseFunc());
    ```
    
    - 결과가 Promise 자체로 반환됩니다.
    
    !https://blog.kakaocdn.net/dn/bXprRH/btrozjJiPVY/u3JnEYljMfVLDTRalkKBQK/img.jpg
    

### 4) ES7 (2016년)

자바스크립트는 2015년 이 후 빠르게 발전하기 시작했고, 매년 표준을 발표하기 이르렀다. ES7은 ECMAscript 2016이라고도 하며, 제곱연산자 (**)와 Array.includes가 적용되었다.

### 5) ES8 (2017년)

Promise가 등장했던 것만큼 중요한 async, await가 적용되었다. 이 후 나오는 ES표준은 편의상 ES.Next 또는 ECMAScript 2017+라고 부른다.

### 6) ES2023

**`toReversed`**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6ebc39d3-135a-4fbb-bcd5-959be4b549bd/Untitled.png)

### `toSplice`

기존의 Splice는 삭제된 항목을 반환하고,

원본을 수정하였다.

```
const a = ["a","b","c","d"];
a.splice(1,2) // ["b","c"]
console.log(a) // ['a','d']
```

toSplice는 기존의 배열을 유지하고, 삭제한 배열을 반환하지 않으며

복사본에서 삭제하여 반환한다.

```
const a = ["a","b","c","d"]
const newArray = a.toSpliced(1,2)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66c8d077-c61d-43fb-8153-fe761fbb28c1/Untitled.png)

### `with`

```
const x = ["a","b","c","e"]
x[3] = "d"
console.log(x) // ["a","b","c","d"]
```

위 방식처럼 기존의 배열값을 수정할 수 있다.

하지만 기존의 배열이 변하여서 아쉬웠다.

with을 사용하면 원본을 지킬 수 있다.