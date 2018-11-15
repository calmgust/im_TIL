# React



## 1. Hello World



React 예제

```jsx
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

***이 코드는 페이지에서 헤더의 "Hello world!"를 렌더링***



요소와 컴포넌트 같은 React 앱의 구성 블록

재사용 가능한 작은 조각으로 복잡한 앱을 만들 수 있다





## 2. JSX 소개



```jsx
const element = <h1>Hello, world!</h1>;
```

문자열도 HTML도 아님

이 문법은 ***JSX <u>(JavaScript의 문법 확장)</u>***

<u>JSX를 리액트와 함께 사용하여 UI가 실제로 어떻게 보일 지 설명하는 것을 권장</u>

JSX는 템플릿 언어처럼 보이지만 JavaScript를 기반으로 하고 있음



#### JSX에 표현식 포함하기

***JSX 안에 <u>JavaScript 표현식</u>을 중괄호로 묶어서 포함시킬 수 있습니다.***

```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = ( // 괄호로 묶는 것?(1)
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render( // 괄호로 묶는 것?(2)
  element,
  document.getElementById('root')
);
```

가독성을 좋게 하기 위해 JSX를 여러줄로 나눴습니다. 필수는 아니지만 이 작업을 수행할 떄 *<u>자동 세미콜론 삽입</u>*을 피하기 위해 **괄호로 묶는 것이 좋습니다.**



#### JSX 또한 표현식이다

컴파일이 끝나면 <u>***JSX 표현식***</u>이 **정규 자바스크립트 함수 호출이 되고 자바스크립트 객체로 인식됩니다.**

이 말은 `if`문이나 `for`반복 내에서 JSX를 사용할 수 있으며, 변수에 할당하거나 매개 변수로 전달하거나 함수에서 반환할 수 있음을 의미합니다.

```jsx
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```



#### JSX 속성 정의

속성에 ***따옴표***를 이용해 문자열 리터럴을 정의할 수 있습니다.

```jsx
const element = <div tabIndex="0"></div>; // 따옴표
```



속성에 ***중괄호***를 이용해 자바스크립트 표현식을 포함시킬 수 있습니다.

```jsx
const element = <img src={user.avatarUrl}></img>; // 중괄호
```



속성에서 자바스크립트 표현식을 포함시킬 때 중괄호를 따옴표로 묶지 마세요. 따옴표 (문자열 값인 경우) 또는 중괄호 (표현식인 경우) 중 하나를 사용해야 하며, 둘 다 같은 속성에 사용할 수 있는 게 아닙니다.



**경고:**

JSX는 HTML보다는 자바스크립트에 가깝기 때문에, React DOM은 HTML 속성 이름 대신 `camelCase` 속성 이름 컨벤션을 사용합니다.

예를 들어, JSX에서 `class` 는 [`className`](https://developer.mozilla.org/en-US/docs/Web/API/Element/className) 이 되며, `tabindex` 는 [`tabIndex`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/tabIndex)가 됩니다.



#### JSX 자식 정의

만약 태그가 비어있다면, XML처럼 `/>`를 이용해 닫아주어야 합니다.

```jsx
const element = <img src={user.avatarUrl} />; // />
```

JSX 태그는 자식을 가질 수 있습니다.

```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
); // <div> 태그 안에 <h> 태그
```



#### JSX 인젝션 공격 예방

유저 입력을 JSX 내에 포함시키는 것이 안전합니다.

```jsx
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```

기본적으로, React DOM은 렌더링 되기 전에 JSX 내에 포함된 모든 값을 [이스케이프](http://stackoverflow.com/questions/7381974/which-characters-need-to-be-escaped-on-html) 합니다. 따라서 어플리케이션에 명시적으로 작성되지 않은 내용은 절대 삽입할 수 없습니다. 모든 것은 렌더링 되기 전에 문자열로 변환됩니다. 이렇게 하면 [XSS (cross-site-scripting)](https://en.wikipedia.org/wiki/Cross-site_scripting) 공격을 막을 수 있습니다.



#### JSX 객체 표현

Babel은 JSX를 `React.createElement()`호출로 컴파일합니다.



아래 두 예제는 동일합니다.

예제1)

```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

예제2)

```jsx
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```



`React.createElement()`는 버그 없는 코드를 작성하는데 도움을 주는 몇가지 체크를 하지만 기본적으로는 아래와 같은 객체를 생성합니다.

```jsx
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};
```

이 객체는 "React elements"라고 부릅니다. 화면에서 볼 수 있는 내용에 대한 설명으로 생각할 수 있습니다. React는 이 객체를 읽어들이고 이를 사용하여 DOM을 구성하고 최신 상태를 유지합니다.



**팁:**

ES6 및 JSX 코드가 모두 올바르게 표시되도록 선택한 편집기에 [“Babel” 언어 설정](http://babeljs.io/docs/editors) 을 사용하는 것이 좋습니다. 이 웹사이트에서는 호환 가능한 [Oceanic Next](https://labs.voronianski.com/oceanic-next-color-scheme/) 컬러 스킴을 사용합니다.





## 3. 요소(*element*) 렌더링

<u>***element***는 React 앱의 가장 작은 구성 블록입니다.</u>

```jsx
const element = <h1>Hello, world</h1>;
```

브라우저 DOM 요소와 달리 ***React 요소(element)***는 순수한 객체이며 생성 비용이 저렴합니다.

React DOM은 React 요소와 일치하도록 DOM을 업데이트합니다.



**Note:**

요소를 “컴포넌트”라는 더 널리 알려진 개념과 혼동할 수 있습니다. [다음 섹션](https://reactjs-kr.firebaseapp.com/docs/components-and-props.html)에서 컴포넌트에 대해 소개합니다. 요소는 구성요소가 “무엇으로” 이루어졌는 지, 그리고 다음으로 넘어가기 전에 이 섹션을 읽는 게 좋습니다.



##### => *요소(element)*와 *컴포넌트(component)*는 다른 개념이니 혼동하지 말자



#### DOM에서 요소(element) 렌더링하기

HTML 파일 어딘가에 `<div>`가 있다고 가정해봅시다.

```jsx
<div id="root"></div>
```

React DOM에 의해 관리되는 모든 것이 이 요소 안에 들어가므로 이걸 **"루트" DOM 노드**라고 부릅니다.

React로 구축한 어플리케이션은 **보통 단일 루트 DOM노드**를 가집니다. React를 기존 앱에 통합하는 경우 **원하는 만큼 많은 분리된 루트DOM 노드**가 있을 수도 있습니다.

React 요소를 루트 DOM 노드에 렌더링하고 싶다면, `ReactDom.render()`에 둘 다 전달하면 됩니다.

```jsx
const element = <h1>Hello, world</h1>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```



#### 렌더링된 요소 업데이트

React 요소(element)는 ***변경 불가능*** 합니다. 한번 요소를 만들었다면, 그 자식이나 속성을 변경할 수 없습니다. 요소는 영화의 단일 프레임과 같습니다. 특정한 시간대의 UI를 보여줄 뿐입니다.

이 지식을 바탕으로 하면, UI를 업데이트할 수 있는 유일한 방법은 새로운 요소를 만드는 것이며, 이 요소를 `ReactDOM.render()`로 전달하는 것입니다.



예제) 시간이 깜빡이는 예제

```jsx
function tick () {
    const element = (
        <div>
            <h1>Hello, world!</h1>
            <h2>It is {new Date().toLocaleTimeString()}.</h2>
        </div>
    );
    ReactDOM.render(
   		element,
        document.getElementById('root')
    );
}

setInterval(tick, 1000);
```

이 예제는 `setInterval()`콜백을 이용해 매 초마다 `ReactDOM.render()`를 호출하고 있습니다.



**Note:**

실제로 대부분의 React 어플리케이션은 `ReactDOM.render()` 를 한번만 호출합니다. 다음 섹션에서는 이러한 코드가 어떻게 [상태 기반 컴포넌트](https://reactjs-kr.firebaseapp.com/docs/state-and-lifecycle.html) 로 캡슐화 되는 지 배울 것입니다.

서로가 서로에게 연관성이 있기 때문에 이 주제를 건너뛰지 않는 걸 권장합니다.



#### React는 필요한 것만 업데이트한다.

React DOM은 요소와 그 자식을 이전 요소와 비교하고, DOM을 원하는 상태로 만드는 데 필요한 DOM 업데이트만 적용합니다.

마지막 예제를 개발자 도구로 확인해보면 관측할 수 있다.

매 틱마다 전체 UI 트리를 설명하는 요소를 만들었지만, 내용이 변경된 텍스트 노드만 React DOM에 의해서 업데이트 됩니다.

이 경험으로 견주어 보았을 때, 시간이 지남에 따라 UI를 변경하는 것이 아니라 주어진 순간을 UI가 어떻게 보여줘야하는 지에 대해 생각하면 버그 전체가 사라집니다.





## 4. 컴포넌트(*component*)와 *props* => 중요



***컴포넌트(component)***를 사용하여 UI를 **독립적**이고 **재사용 가능한 부분으로 분리**하고 각 부분을 독립적으로 생각할 수 있음

개념상 컴포넌트는 자바스크립트 함수와 유사 

***=> 컴포넌트(component) === 함수(function in JavaScript)***

임의의 입력("props"라고 부르는)을 받아들이고 어떤게 화면에 나타나야 하는 지를 설명하는 React 요소를 반환



#### 함수형 및 클래스 컴포넌트

컴포넌트를 정의하는 가장 간단한 방법은 자바스트립트 함수로 작성하는 것

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

이 함수는 단일 "props"(속성을 나타냄) 객체 인수를 받고 React 요소를 반환하기 때문에 유효한 React 컴포넌트 **=> 함수형**

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

***=> ES6 class를 사용 가능***

*위의 두 컴포넌트는 React 관점에서 보면 동일*



#### 컴포넌트 렌더링

이전에는 DOM 태그를 나타내는 React 요소만

```jsx
const element = <div />;
```

요소에 유저가 정의한 컴포넌트를 나타낼 수도

```jsx
const element = <Welcome name="Sara" />;
```

React가 유저가 정의한 컴포넌트를 나타내는 요소를 볼 때 JSX속성을 이 컴포넌트에 단일 객체에 전달 => 이 객체를 "***props***"라고 부릅니다.



예제) "Hello, Sara"를 페이지에 랜더링

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

1. `<Welcome name="Sara" />`요소로 `ReactDOM.render()`를 호출합니다.

2. React가 `{name: 'Sara'}`를 props로 하여 `Welcome` 컴포넌트를 호출합니다.

3. `Welcome`컴포넌트가 그 결과로 `<h1>Hello, Sara</h1>`요소를 반환합니다.

4. ReactDOM이 `<h1>Hello, Sara</h1>`과 일치하도록 DOM을 효율적으로 업데이트합니다.


**Caveat:**

컴포넌트 이름은 항상 대문자로 시작하길 바랍니다.

예를 들어 `<div />` 는 DOM 태그를 나타내지만 `<Welcome />` 은 컴포넌트를 나타내며 스코프에 `Welcome` 을 필요로 합니다.



#### 컴포넌트 결합

컴포넌트는 출력될 때 다른 컴포넌트를 참조 가능

이를 통해 세부 레벨에서 동일한 컴포넌트 추상화를 사용 가능

React 앱에서는 버튼, 폼, 다이얼로그, 스크린 같은 것들은 모두 일반적으로 컴포넌트로 표현



예제) `Welcome`을 여러번 렌더링하는 `App`컴포넌트를 만들 수 있음

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

<u>일반적으로, **새 React 앱은 단일 `App` 컴포넌트를 최상위에** 둡니다.</u>

그러나 <u>기존 앱에 React를 도입하는 경우, `Button`같은 **작은 컴포넌트로부터 덩치를 키워나가기 시작하여 점차적으로 뷰 계층의 최상단으로** 나아갈 수</u> 있습니다.



#### 컴포넌트 추출

컴포넌트를 더 작은 컴포넌트로 쪼개는 것을 두려워하지 마십시오



예제) `comment`컴포넌트

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

이 컴포넌트는 `author`(객체),  `text`(문자열),  `date`(date)를 props로 받고, 소셜 미디어 웹사이트의 덧글을 나타냅니다.

이 컴포넌트는 **중첩 때문에** <u>변경하기 까다로울 수 있으며, 각 파트를 다시 사용하기도 어렵기 때문</u>에 **컴포넌트를 추출**



**`Avatar`를 추출**

```jsx
function Avatar (props) {
    return (
        <img className="Avatar" 
            src={props.user.avatarUrl}
            alt={props.user.name}
        />
        
    );
}
```

`Avatar`는 `Comment`내에서 렌더링되는 지 알 필요가 없습니다. 따라서 속성을 `author` 대신 `user`라는 더 일반적인 이름을 사용

***컴포넌트가 사용되는 상황이 아닌 컴포넌트 자체 관점에서 props 이름을 짓는 것을 권장***



**`Comment`를 단순화**

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
		<Avatar user={props.author} /> <!---->
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```



**`UderInfo`컴포넌트를 추출**

```jsx
function UserInfo (props) {
    return (
        <div className="UserInfo">
        	<Avatar user={props.user} />
            <div className="UserInfo-name">
            	{props.user.name}
            </div>
        </div>
    );
}
```



**`Comment`를 단순화**

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={user.author} /> <!---->
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

컴포넌트를 추출하는 것은 처음에는 쓸데없는 일처럼 보일 수 있지만 재사용 가능한 컴포넌트 팔레트를 사용하면 큰 앱에서 비용을 줄일 수 있습니다.

좋은 규칙은 UI의 일부가 여러번 사용되거나 (`Button`, `Panel`, `Avatar` ), 자체적으로 충분히 복잡하면서 (`App`, `FeedStory`, `Comment`), 재사용 가능한 컴포넌트가 될 후보들



#### props는 읽기전용

컴포넌트를 [함수나 클래스](https://reactjs-kr.firebaseapp.com/docs/components-and-props.html#functional-and-class-components) 중 어떤 걸로 선언했 건, props를 수정할 수 없습니다. `sum` 함수를 살펴봅시다.

```jsx
function sum (a, b) {
    return a + b;
}
```

일부 함수는 입력을 변경하려 하지 않고 항상 동일한 입력에 대해 동일한 결과를 반환하기 때문에 [“순수”](https://en.wikipedia.org/wiki/Pure_function) 함수라고 부릅니다.



대조적으로, 이 함수는 입력을 변경하기 때문에 순수하지 않습니다.

```jsx
function withdraw(account, amount) {
  account.total -= amount;
}
```



***모든 React 컴포넌트는 props와 관련한 동작을 할 떄 순수 함수처럼 동작해야한다.***



##### state

 ***state는 React 컴포넌트가 이 규칙을 어기지 않고 유저 액션, 네트워크 응답, 기타 등등에 대한 응답으로 시간 경과에 따라 출력을 변경할 수 있게 합니다.***





## 5. State와 라이프사이클



`ReactDOM.render()`을 호출하여 렌더링된 출력을 변경

```jsx
function tick() {
  const element = ( <!---->
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2> <!---->
    </div>
  );
     
<!---->
  ReactDOM.render(
  element,
  document.getElementById('root')
  );
<!---->
}

setInterval(tick, 1000);
```



재사용 가능하고 캡슐화된 `Clock`컴포넌트를 만드는 방법에 대해 학습

시계가 어떻게 보이는 지 캡슐화하는 것부터 시작

```jsx
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}     

function tick () {
  ReactDOM.render(
  <Clock date={new Date()} />,
  document.getElementById('root')
  );
}

setInterval(tick, 1000);
```



