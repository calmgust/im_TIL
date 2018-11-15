# React (velopert)



```jsx
class Codelab extends React.Component {
  render () {
    return(
      <div>
            
      </div>
    );
  }
}

class App extends React.Component {
  render () {
    return (
        <Codelab/>
    );
  }
}

ReactDOM.render(<App/>, document.getElementById('root'));
```



### props

* ***컴포넌트 내부의 Immutable Data***
* JSX 내부에 `{this.propspropsName}`
* 컴포넌트를 사용 할 때, <>괄호 안에 `propsName="value"`
* this.props.children은 기본적으로 갖고있는 props로서, `<Cpnt>여기에 있는 값이 들어간다.</Cpnt>`



```jsx
class Codelab extends React.Component {
  render () {
    return(
      <div>
        <h1>Hello {this.props.name}</h1>
        <div>{this.props.children}</div>
      </div>
    );
  }
}

class App extends React.Component {
  render () {
    return (
      <Codelab name='velopert'>이 사이에 있는 거</Codelab>
    );
  }
}

ReactDOM.render(<App/>, document.getElementById('root'));
```

**=>**

**Hello velopert**

**이 사이에 있는 거** 



```jsx
class Codelab extends React.Component {
  render () {
    return(
      <div>
        <h1>Hello {this.props.name}</h1>
        <div>{this.props.children}</div>
      </div>
    );
  }
}

class App extends React.Component {
  render () {
    return (
      <Codelab name={this.props.name}>{this.props.children}</Codelab>
    );
  }
}

ReactDOM.render(<App name='velopert'>I am your child</App>, document.getElementById('root'));
```

**=>**

**Hello velopert**

**I am your child**





#### 기본 값 설정*

`Component.defaultProps = {...}`

```jsx
class App extends React.Component {
  render () {
    rerturn (
      <div>{this.props.value}</div>
    );
  }
};

App.defaultProps = {
  value: 0
};
```



#### Type 검증*

`Component.propTypes = {...}`

```jsx
class App extends React.Component {
  render() {
    return (
      <div>
        {this.props.value}
        {this.props.secondValue}
        {this.props.thirdValue}
      </div>
    );
  }
};

App.propType = {
  value: React.PropTypes.string,
  secondValue: React.PropType.number,
  thirdValue: React.propTypes.any.isRequired
};
```





### state

* ***유동적인 데이터***
* JSX 내부에 `{this.state.stateName}`
* ***초기값 설정이 필수***, 생성자(constructor)에서 <u>**`this.state = {}`**</u>으로 설정
* 값을 수정할 때에는 <u>**`this.setState({...})`,**</u> 렌더링 된 다음엔 `this.state = `절대 사용하지 말것



```jsx
class Counter extends React.Component {

//-----
  constructor(props) {
    super(props);
    this.state = {
      value:0
    };
    this.handleClick=this.handleClick.bind(this)
  }
  
  handleClick() {
    this.setState({
      value: this.state.value + 1
    });
  }
  
  render() {
    return (
      <div>
        <h2>{this.state.value}</h2>
        <button onClick={this.handleClick}>Press Me</button>
      </div>
    )
  }
}
//-----

class App extends React.Component {
  render() {
    return (
      <Counter />
    );
  }
};

ReactDOM.render(
  <App/>,
  document.getElementById("root")
);
```





#### JavaScript - map

`map()` 메소드는 파라미터로 전달 된 함수를 통하여 배열 내의 각 요소를 처리해서 그 결과로 새로운 배열을 생성합니다.



##### `arr.map(callback, [thisArg])`

* `callback`- 새로운 배열의 요소를 생성하는 함수로서, 다음 세가지 인수를 가집니다.

  * `currentValue`- 현재 처리되고 있는 요소

  * `index`- 현재 처리되고 있는 요소의 index 값

  * `array`- 메소드가 불려진 배열

* `thisArg(선택항목)`- callback 함수 내부에서 사용 할 this 값을 설정



