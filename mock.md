# Mock Interview



## personal question



#### 부트캠프라는 단기 교육을 들은 것 같은데 개발을 배우게 된 자신만의 배경 및 스토리를 이야기 해주세요 (1분내)



#### 단기간의 교육으로 기술적 이해도에 대해 스스로의 열정, 욕심에 대해 알려달라(기술적 방향성)



#### 1) 개발 도메인 & 컴퓨터 영역에서 관심있는 영역?





------



## web general question



#### 웹 서비스 or 웹 어플리케이션을 개발해 보거나 운영해본 경험이 있다면 말씀해 주세요



#### 어떤 웹 서비스 프로토콜을 알고 있습니까?

- http / https(보안을 신경쓴 것)
- ~~https는 호환이 조금 어렵다~~

#### v8에 대해서 알고 있나요? 설명해 보시겠어요?

- V8 엔진은 웹 브라우저를 만드는 데 기반을 제공하는 오픈 소스 자바스크립트 엔진





------



## JavaScript question



#### closure에 대해 설명해주시고 example이 있다면 이야기해주세요

- 외부함수의 변수에 접근 가능한 내부함수 => 함수 선언 시 생성되는 유효범위



#### js에서 this란 무엇이고 어디에 사용되나요

- this는 현재 실행 문맥 => `실행문맥`이란 호출자가 누구냐는 것



#### Difference between "==" and "===" ?

- `==` => Equal Operator / `===` => Strict Equal Operator
- `==` => **값**이 같은지 판단 (true / false)
- `===` => **값**은 물론이고 **타입**과 **형식**까지 같은지 판단 (true / false)



#### ES6에 대해서 알고 계신가요? 사용하고 있는 ES6 feature들을 설명해주세요



#### let과 var의 차이점과 활용도를 알려주세요

- **`var` 선언자**

  - <u>hoisting (***호이스팅***)</u>
  - <u>function level scope가 지원</u>
  - <u>block level scope가 지원되지 않음</u>

- **`let` 선언자**

  - 같은 블럭 내에서 같은 이름의 변수를 중복해서 선언할 수 없음 (***중복 불가***)
  - ***변수를 초기화하기 전에는 변수에 접근할 수 없게 해서 호이스팅을 방지***
  - <u>선언할 변수에 block level scope를 적용</u>

  

#### javascript와 node는 어떻게 다른가요

- javascript는 언어이고
- node는 javascript를 돌리는 환경이다
- 말이야 방구야



#### hoisting에 대해 설명해 주세요

```js
helloMessage = "hello";
console.log(helloMessage);

var helloMessage; // 이 변수 선언은 스코프 최상위로 호이스팅된다.
```

- 호이스팅은 끌어올림의 의미 => 변수가 선언된 위치와 관계없이 ***스코프의 최상위로 끌어올림 되어*** 같은 스코프라면 어디서든 호출됨 (`var` 선언자) => ***코드의 가독성을 떨어뜨림***
  - **`var` 선언자의 특징** 
    - <u>hoisting (호이스팅)</u>
    - <u>function level scope가 지원</u>
    - <u>block level scope가 지원되지 않음</u>
- 이러한 특성을 방지하기 위하여 `let` 선언자가 나옴 ***=> 호이스팅을 방지할 수 있다***
- `let / const` 가 호이스팅 되지 않는 것이 아니라 
- `let / const`선언 변수는 호이스팅되지 않는 것이 아니다. 스코프에 진입할 때 변수가 만들어지고 **TDZ(Temporal Dead Zone)**가 생성되지만, 코드 실행이 변수가 실제 있는 위치에 도달할 때까지 액세스할 수 없는 것이다. `let / const`변수가 선언된 시점에서 제어흐름은 `TDZ`를 떠난 상태가 되며, 변수를 사용할 수 있게 된다.
- let 변수를 초기화하기 전에는 변수에 접근할 수 없기 때문에 호이스팅이 방지



#### call / apply / bind에 대해 설명해 보세요 언제 다르게 쓰나요?

- `function.prototype.call`은 **파라미터 중 첫 번째 인자**를, 함수 내부에서 사용할 `this`로 만들어 준다.
- `function.prototype.apply`는 **파라미터를 배열 형태**로 받는다.
- `function.proptotype.bind`는 **원하는 Function에 인자로 넘긴 `this`가 바인딩** 된 새로운 함수를 리턴한다.



```js
(function() {console.log(1);
            setTimeout(function(){console.log(2)}, 1000);
            setTimeout(function(){console.log(3)}, 0);
            console.log(4);})(); 
```

#### 실행하면 결과가 어떻게 나오나요? 왜 그런가요?

- 1, 4, 3, 2
- 2, 3은 비동기



#### ~~javascript array가 c언어의 array와 어떻게 다른지 설명해주세요~~



#### <u>deep과 shallow object copy에 대해 설명해 주시고 용도가 있다면 말씀해주세요</u>



#### <u>javascript의 null, undefined, undeclared 차이점은 무엇인가요</u>

- **`null`** => 빈 객체라는 의미 (변수에 값을 나타내지 않도록 지정 가능 (할당 값))
- **`undefined`** => 변수는 선언되었지만 값이 할당되지 않았을 때
- **`undeclared`** => 변수가 선언되지 않음 (`ReferenceError` 발생)



#### 모든 자바스크립트 파일을 브라우저에서 한번에 loading 할 때 문제점

- 싱글스레드



#### 자바스크립트 Prototype에 관해 설명해주세요 (상속)



<u>Array prototype splice와 slice의 차이점은 무엇인가요</u>



#### <u>promise에 대해서 설명해주세요</u>

- 프로미스는 자바스크립트 비동기 처리에 사용되는 객체
- 여기서 자바스크립트의 비동기 처리란 '특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성'을 의미



#### OOP의 4가지 특징과 javascript를 활용하여 OOP적으로 어떻게 개발할 수 있을지 설명해 보세요

- oop: 객체지향 프로그래밍(object-oriented programming, oop)
  1. 추상화
  2. 캡슐화
  3. 상속
  4. 다형성



#### 익명함수와 선언적함수의 차이가 무엇인가요

- ***익명함수***: function(){}형태는 함수지만 이름을 가지고 있지 않으므로 익명함수라고 부름
  - <u>이름이 없으므로 변수에 넣어 사용해야 함</u>
  - 익명함수를 먼저 선언한 후 호출을 할 수 있음. test1() <- 함수를 호출. 이 문장이 익명함수의 항상 뒤에 와야 함.
    - `var test1 = function(){}`
- ***선언적 함수***: function 이라는 키워드를 사용하여 함수를 선언하는 것
  - 선언적 함수를 호출할 땐 선언적 함수의 전에 와도 호출이 됨. test2() 이건 선언적 함수의 앞이든 뒤든지 써도 상관없음
  - 선언적 함수인 경우 스크립트 태그를 실행하기 전 가장 먼저 읽기 때문
    - function test2(){}



#### Can you describe the main difference between a forEach loop and a .map() loop and why you would pick one versus the other?



#### 타입스크립트에 대해서 들어보셨나요? 사용해 본 경험은? 어떻게 다른가요? 장점은?

- ECMAScript채택해서 개발하기 때문에 JavaScript와 호환이되고 자바스크립트의 단점을 보완해준다
- 타입을 선언(미리 지정)해주기 때문에 타입체크를 해줄 수 있어서 타입 오류를 사전에 방지 할 수 있다



- 타입스크립트를 채택하고 있는 회사에서는 반드시 질문을 받을 수 있다



#### 크롬브라우저의 ES6 스펙 지원이 되지 않는 브라우저의 경우 개발자로서 해결 방법은?

- 컴파일링 혹은 트랜스파일링은 이용해서 ????





------



## nodejs question



#### nodejs가 무엇인가요? 어디에 사용할 수 있나요?



#### 다른 개발환경이 아닌 nodejs를 사용해야 하는 장점이 무엇인가요?



#### 왜 nodejs는 single-threaded인가요



#### nodejs에서 callback을 설명해보세요



#### nodejs에서 비동기란 무엇인가요



#### nodejs callback hell이 무엇인가요? 어떻게 이를 피할 수 있을까요?



#### <u>nodejs에서 module이란 무엇인가요?</u>



#### nodejs에서 event loop이란 무엇인가요? nodejs에서 비동기 처리를 그림으로 그려서 설명할 수 있나요?



#### chrome이랑 node.js 환경 다른점 + 두 환경 모두에서 동일하게 돌아가나요? 브라우저 환경에서는 어떻게?



#### express는 무엇인가요? 무엇을 해주나요?



#### package.json의 역할은 무엇인가요?

- npm 의존성 모듈을 관리하는 역할





------



## data structure



#### array vs linked list 비교해서 설명해 보세요



#### stack vs queue 비교해서 설명해 주세요

- ***stack*** => 뒤로 들어와서 뒤로 나온다 (***last in - first out***)
- ***queue*** =>  뒤로 들어와서 앞으로 나온다 (***first in - first out***)



#### HashTable을 설명하고 사용 예를 말씀해 주세요





------



## algorithm question



#### 54321 배열이 주어졌을 때 어떤 sort를 쓰겠는가. 왜?

- binary sort

#### random으로 배열된 숫자들이 있을 때 어떤 sort를 쓰겠는가 왜?

- merge sort

#### insertion sort가 일어나는 과정 설명



#### quick sort가 일어나는 과정 설명



#### DFS vs BFS?





------



## HTTP question



#### HTTP request에는 어떤 것들이 있나요? 리스트업 해주시고 설명해주세요



#### 브라우저 URL을 입력하고 요청한 페이지를 볼때까지 어떤 일이 일어나는가?



#### HTTP 요청과 응답 헤더에 어떤 내용이 들어가는가?



#### HTTP와 HTTPS 프로토콜의 차이점은 무엇인가?

- 보안

#### URL 축약서비스 (bit.ly와 같은 url shortenr)를 어떻게 설계하겠는가?



#### CORS란 무엇인가요? CORS의 목적과 CORS 활용에 대해 이야기해주세요

- orgin(nase url)이 다르기 때문에 CORS를 사용 => 이름 그대로 (이름 체킹)

#### 대표적인 서버 응답 코드에 대해 설명해 주세요





------



## network general



#### OSI 7, 5 layer 네트워크에 대해서 들어보셨다면 설명해주시겠어요?



#### CDN의 장점과 단점에 대해 알고 계신가요?



#### forward proxy vs reverse proxy?





------



## Database question



#### 왜 Database를 사용해야 하는 가요?



#### SQL vs NoSQL에 대해 설명해주세요 어떤 목적으로 어떤 database type이 유리할까요?



#### CRM 사용의 장점과 단점은?



#### SQL database 설계에 있어 중요하게 생각하는 점은?



#### database indexing이란 무엇이며 왜 하는가요?

답변을 못했던 질문

database indexing에 대해 공부 필요



#### transaction이란 무엇이며 왜 하는가요?



#### SQL injection이란 무엇이며 어떻게 막을 수 있을까요?



#### 사용자의 비밀번호는 어떻게 저장하나요?

hashing 필요!!





------



## Cloud infra question



#### 왜 배포가(deploy)가 중요한가요? 웹 개발자가 알아야 하는 이유는 무엇일까요?



#### 사용해 본 클라우드 인프라 서비스에 대해 소개해 주세요



#### AWS S3, EC2 서비스 블록에 대해 설명해 주세요



#### DNS에 대해 설명해 주세요



#### 본인이 가장 즐겨 사용하는 클라우드 서비스 블록에 대해 설명해 주세요



#### CI/CD에 대해 들어보셨나요? 소개해 주세요



#### monolithic vs micro service architecture





------



## Development question



#### 본인이 웹 application (full stack)을 개발한다고 했을 때 간단한 work flow를 설명해 주세요



#### unit test 경험이 있나요? unit test, TDD가 왜 중요한가요? 단점도 있을까요?



#### What is the difference between a unit test and a function / integration test?



#### What is the purpose of a code style listing tool?



#### 본인은 Refactoring은 언제, 왜, 어떻게 하나요?

Refactoring의 필요성!!



#### agile scrum 경험이 있는 것 같다. agile scrum에 대해 소개를 해 주시고, 본인이 경험한 scrum의 장점과 단점에 대해 공유해 주세요



#### 개발을 하며 문서화, 개발 wiki 경험이 있는지? 본인이 생각하는 문서화의 목표는?



#### git commit 할 때 지키는 rule?



#### git repository README에는 어떤 내용들이 들어가야 하나요?



#### 어떤 코드가 좋은 코드인가요? 본인이 생각하는 clean code란?



#### 견고(ronust)한 코드, 소프트웨어란 무엇인가요?



#### 팀으로 개발할 때 지향하는 자신만의 특징?



#### 팀 협업에서는 무엇이 제일 중요하다고 생각하시나요?

- 커뮤니케이션
- 실력을 떠나서 각각의 팀원의 강점을 서로 인지하여 최상의 퍼포먼스를 이끌어내는 방법은 커뮤니케이션이라고 생각

#### MVP 디자인 패턴에 대해 설명해 주시고 사용해 본 경험이 있는지 공유 해주세요



#### 자신이 경험한 git 협업 flow에 대해 설명해보세요



#### 본인이 알고 있는 error handling의 종류와 경험을 말씀해 주세요



#### 오픈소스 라이브러리를 선택하는 기준은 무엇인가요?

비교적 최신의 라이브러리 / 지속적인 관리? 지속적인 업데이트가 이루어지고 있는 라이브러리



#### DRY(Don't Repeat Yourself)를 설명하고, 내가 활용한 사례가 있다면?



#### 모듈화가 무엇이며 모듈화를 통해 얻는 이익은?

- 코드의 재사용으로 불필요한 코드를 줄일 수 있다.



------



## Backend Question



#### Restful api란? 사용 시 장점과 단점은?



#### session - cookie 방식과 토큰(JWT) 방식의 차이점에 대해 이야기 해보세요

프론트 엔드를 지원하더라도 이해가 필요한 부분이라고 생각

특히 로그인의 경우





------



## Frontend question



#### <u>Describe the difference between a cookie, sessionStorage and localStorage</u>

- cookie 클라이언트에 대한 정보를 이용자의 pc의 하드디스크에 보관하기 위해서 웹 사이트에서 클라이언트의 웹 브라우저에 전송하는 정보 (통행증)
- web storage는 쿠키의 단점을 보완해서 만든 기술
- local storage 영구적 보관 가능
- session storage 세션이 종료되면(웹 브라우저를 닫을 경우) 클라이언트에 대한 정보를 삭제



#### 브라우저 동작 원리에 대해 설명해 보세요

- DOM tree 구축 => 렌더 트리 구축 => 렌더 트리 배치 => 렌더 트리 그리기



#### <u>client side rendering vs server side rendering</u>



#### bundling이 무엇이며 왜 필요한가요? 본인이 경험한 bundling을 소개해주세요, 무슨 툴을 쓰셨나요?



#### <u>프론트엔드 입장에서 신경써야 할 보안은 무엇들이 있을까요? + CSRF가 무엇이며 어떻게 하면 막을 수 있나요? + XSS가 무엇이며 어떻게 하면 막을 수 있나요? + CORS에 대해 설명해 보세요 + JSONP를 알고 있나요? 왜 필요하며 특징은 무엇인가요?</u>



#### <u>리액트란 무엇인가요? 다른 JS프레임워크와 어떤 특징, 차별점이 있나요?</u>

- 리액트는 라이브러리다

#### react state and props에 대해 설명해 보세요

- state
- props

#### 리액트에 있는 라이프사이클들을 이야기해보고, 각 라이프사이클은 어떤 용도로 유익할지 설명해 보세요



#### react router와 같은 client side routing에 대해 설명해 주세요



#### What can you tell me about JSX?

- JSX는 리액트에서 사용되는 문법
- 컴파일링이 되면서 최적화되기 때문에 속도가 빠르다

#### flux cs mvc?



#### redux에 대해 설명해 보세요

- 리덕스는 어플리케이션의 클라이언트쪽 `state` 를 관리하기 위한 거대한 이벤트 루프
- 액션 = 이벤트
- 리듀서 = 이벤트에 대한 반응



#### lazy loading이란?



#### SPA는 기존 웹사이트와 무엇이 다른가요?



#### AJAX 기술에 대해 설명해 보세요



#### script tag의 위치와 위치에 따라 고려해야 하는 점은 무엇인가요



#### 이벤트 버블링이란 무엇인가요? 어떻게 막을 수 있나요?



#### CSS보다 SCSS/SASS가 가지고 있는 장점은?



#### id와 class selector는 어떻게 다르게 쓰이나요?



#### css box model에 대해 말해보세요

- content - padding - border - margin



#### css에서 em, px, rem의 차이점에 대해 이야기 해보세요





------



## Personal question



#### 컴퓨터, 웹 기술에 대해 본인이 가장 흥미를 가지는 분야는



#### 요구사항대로 만들어 내는 개발자와 서비스를 이해하는 개발자는 어떻게 다르다고 생각하시나요?



#### 일이 과할 때 어떻게 일을 처리하시나요?



#### 회사 기술 스택에 맞추어 단기간 내에 언어와 프레임워크를 학습하여야 할 때, 어떻게 공부하고 해결할 것인가?



#### 본인이 생각하는 좋은 소프트웨어 개발자의 상은 무엇인가요?



#### 워라벨에 대한 개인적인 입장은?





------



## etc



#### 왜 개발자가 되고 싶으세요?



#### 최근 본인이 가장 관심있어하는 웹 기술이 있나요? 상세히 설명해 주시고 관심을 어떤 식으로 발전시키고 있나요? (블로깅, 밋업, 컨퍼런스, 유투브 세미나 시청, 공부 등등)



#### 10년 뒤에 되고 싶은 그림이 있나? or 5년 (엔지니어든 뭐든)



#### 거절을 잘 못하시나요? 자신의 의사가 NO일 때 NO라고 말할 수 있으신가요?

상황에 따라 다르다

불필요한 일에 따른 나의 의사 NO일 경우 NO라고 말하기가 쉽지만

필요한 일에 따른 나의 의사가 NO일 경우 NO라고 말하기가 쉽지 않다



#### 왜 저희 회사에 지원하시게 되었나요?



#### 회사에 대해 궁금한 점?

반드시 질문을 해야되는 부분