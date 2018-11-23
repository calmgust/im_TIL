# Article Collector



Article Collector는 웹사이트에 대한 출력 결과 (HTML의 내용을 가공하여 file)를 수집하는 형태의 프로그램



1. 수집하려는 URL을 source list에 입력
2. 서버가 각각의 URL을 https로 요청한 후
3. 응답을 받아와 저장한 후에 출력



***file 읽기 및 저장, 그리고 컨텐츠를 수집하는 과정을 구현하고 이를 REST API로 호출***





## 1. Structure

데이터를 저장할 용도의 data 폴더

data 폴더 아해의 파일 내용



* **`source.txt`**: 받아올 사이트의 주소를 담는 파일

  `/api/source` HTTP 요청을 통해 이 파일의 내용을 읽고 쓰기가 가능

  (현재 Article Collector는 Medium이라는 블로깅 서비스의 내용만 받기가 가능

  => `src/server/routes/data.js` 의 POST 요청 부분을 살펴보면, Medium HTML 구조 중에서, 작성된 글을 담고 있는 특정 selector를 추출하는 것을 볼 수 있음)

* `0.txt`, `1.txt`, `2.txt`, `...` : URL을 통해 article의 수집이 완료되면, `source.txt` 의 index에 따라 고유의 파일이름을 갖고, 관련 내용이 저장

```js
const sourceRouter = require('./routes/source');
const dataRouter = require('./routes/data');
// 생략
app.use('/api/source', sourceRouter);
// http://localhost:3000/api/source 관련 내용이 sourceRouter에 담겨 있습니다.

app.use('/api/data', dataRouter);
// http://localhost:3000/api/data 관련 내용이 dataRouter에 담겨 있습니다.
```





### Getting Started

- `npm install` (또는 `yarn install`) 명령을 통해 이 Sprint에 필요한 dependency를 설치합니다.
- Sprint 진행은 `npm run dev` (또는 `yarn dev`)로 개발 서버를 띄워놓고 파일을 수정하면 nodemon에 의해 자동적으로 반영이 됩니다. (아래에 설명합니다)
- `npm test` (또는 `yarn test`)를 통해 하나하나 테스트를 통과하세요.

`package.json`에 기술된 각각의 dependency에 대한 대략적인 설명은 다음과 같습니다. 특별히 중요하게 생각해볼 라이브러리는 굵은 색 글씨로 표시했습니다.





### Server-side Dependencies

- **express**: API 작성을 위해 server-side에서 사용할 수 있는 *framework*
- [body-parser](https://github.com/expressjs/body-parser): express에서 HTTP 요청시 같이 전달되는 body를 JSON 혹은 텍스트 등으로 파싱하는 middleware (middleware는 다음 스프린트때 설명합니다)
- [jsdom](https://github.com/jsdom/jsdom): node.js에서는 `window` 객체나 `document`객체가 없습니다. 그러나 경우에 따라 DOM을 다루어야 할 일이 있을 수 있습니다. jsdom은 node.js 환경에서 HTML string을 바탕으로 DOM object를 만들어 element를 다룰수 있게 만들어주는 라이브러리입니다.
- **nodemon**: node.js로 작성한 코드가 변경될 때 자동으로 프로그램을 재시작하게 해주는 유틸리티





### Notes: web pack & bundler (Client-side Dependencies)



Recent.ly 작성 시에, 각각의 파일을 `window` 객체에 노출시켜줌으로 파일 단위로 컴포넌트 구분을 할 수 있도록 도와주는 것

이렇게 전역변수를 추가해주는 것은 좋은 방법이 아님



**대안**

#### ***CommonJS spec***

`require`, `exports`

이에 대한 반응으로 **browserify / webpack / parcel** 등의 Bundler(building tool)이 등장

***webpack***은 building tool로서, create-react-app의 표준 번들러이면서 가장 대중적인 번들러



#### ***Node.js Module***





## 2. Helper function

Node module의 사용에 익숙해지기



#### ***fs module / http module***



#### ***async / await***

```js
async function foo() { }
foo.construtor; // ƒ AsyncFunction() { [native code] }
foo(); // Promise
```

**async function의 constructor는  `AsyncFunction`이며 실행은 `promise` 를 리턴**

Helper function에서는 `fs`,`https`에서 사용하는 callback을 Promise의 형태로 전환시켜 리턴하여야 합니다. 이 경우에는 routing 코드에서 `await` keyword를 사용하기 위해서 이와 같이 작성합니다. 물론 `await` 대신에 `.then`과 `.catch` 등의 Promise 패턴을 사용할 수도 있습니다. `resolve`와 `reject`를 어떻게 사용해야하는 지 이해하고, 이 패턴에 익숙해지세요.

 