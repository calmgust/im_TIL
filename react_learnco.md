# React (learnco)



***React***는 <u>페이스북에서 개발한 오픈소스 라이브러리</u>

웹 개발을 위한 프레임워크 혹은 라이브러리로는 **Backbone, Angular, Vue, React** 등



##### React는 크게 네 가지

#### JSX / props / state / Life Cycle





### JSX

JSX는 XML형식으로 JavaScript를 작성하는 방식



ex)

```javascript
React.createElement('div', {className:'red'}, 'Children Text');
```

이 코드를 JSX로 바꾸면,

```jsx
<div className='red'>Children Text</div>;
```

***매우 간결해지므로 JSX를 꼭 사용***





### props

***props는 컴포넌트(component)가 갖는 속성 값***



##### *  *Component* => JSX태그로 감싸진 녀석들은 모두 Component



```jsx
<div className='red'>Children Text</div>;
```

div라는 컴포넌트가 red라는 className을 갖고 있는 형태

**<u>참고로 html의 class를 React에서는 className으로 씁니다.</u>**



마치 html의 attribute를 쓰듯이 작성

조금 다른 점은 **prop에 문자열을 대입하는 경우를 제외하고는 중괄호로 감싸줍니다.**

```jsx
const myProp = {a:1, b:2};

<div className="red" myProp={myProp}>Children Text</div>
```





### state

***state는 해당 컴포넌트의 상태 (하나의 객체로 표현)***

***props***는 **컴포넌트를 사용**할 때 넘겨주지만, ***state***는 **컴포넌트를 정의**할 때 작성



state가 변하면 re-render를 하기 때문에 해당 컴포넌트를 다시 그리게 됩니다.

코드를 보면서 확인





### Life Cycle

React의 생명주기



***React component가 생성(Mount)되었다가 사라지는(Unmount) 주기***

![2018-11-13 19 21 19](https://user-images.githubusercontent.com/40155174/48407160-8ac49c00-e779-11e8-9644-2f751202b4a7.png)



