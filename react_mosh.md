# Mosh(React)



#### jsx 

#### rendering list 

#### conditional rendering 

#### handling event 

#### updating the states



## Components



#### components (1 - 8)

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    count: 1,
    // imageUrl: 'https://picsum.photos/200',
    tags: ['tag1','tag2','tag3'],
  };

  styles = {
    fontSize: 30,
    fontWeight: 'bold'
  }

  render() { 
    // let classes = this._getBadgeClasses(); // ctrl + shift + R
    return (
      <React.Fragment>
        {/* <img src={this.state.imageUrl} alt="" /> */}
        {/* <span>{this.state.count}</span> */}
        <span style={this.styles} className={this._getBadgeClasses()}>{this._formatCount()}</span>
        <button style={{fontSize:30}}className="btn btn-secondary btn-sm">Increment</button>
        <ul>
          { this.state.tags.map((tag) => <li key={tag}>{ tag }</li>) }
        </ul>
      </React.Fragment>
    );
  }

  _getBadgeClasses() {
    let classes = "badge m-2 badge-";
    classes += (this.state.count === 0) ? "warning" : "primary";
    return classes;
  }

  _formatCount() {
    const { count } = this.state;
    // return this.state.count === 0 ? 'Zero' : this.state.count;
    return count === 0 ? 'Zero' : count;
    // return count === 0 ? <h1>Zero</h1> : count;
  }

}
 
export default Counter;

// export default class Counter extends Component {
//   render() { 
//     return <h1>Hello World</h1>;
//   }
// }
```





#### consitional rendering

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    count: 1,
    tags: [],
  };

  renderTags() {
    if (this.state.tags.length === 0) return <p>There are no tags!</p>;

    return <ul>{this.state.tags.map(tag => <li key={tag}>{tag}</li>)}</ul>;
  }

  render() { 
    return (
      <React.Fragment>
        {this.state.tags.length === 0 && 'Please create a new tag!'}
        {/* => 'Please create a new tag!' */}
        {this.renderTags()}
      </React.Fragment>
    );
  }

}
 
export default Counter;

```





#### Handling event

```jsx
class Counter extends Component {
    state = {
        count : 0,
    };

    handleIncrement = () => {
		console.log('Increment Clicked', this.state.count);
    }
    
    render() {
        return(
        	<React.Fragment>
            	<button
                    onClick={this.handleIncrement} //
                    className="btn btn-secondary btn-sm"
                >
                    Increment
                </button>
            </React.Fragment>	
        );
    }
}
```

`onClick={this.handleIncrement}` 함수 실행?





#### Binding Event Handlers

```jsx
class Counter extends Component {
    state = {
        count: 0,
    }

    constructor() {
        super();
        this.handleIncrement = this.handleIncrement.bind(this); // binding 해줘야 한다
    }

    handleIncrement() {
        console.log('Increment Clicked', this.state.count);
    }

}

//-----

class Counter extends Component {
    state = {
        count: 0,
    }

    handleIncrement = () => { // arrow function은 binding을 해줄 필요가 없다!!
        console.log('Increment Clicked', this.state.count)
    }
}
```

***`obj.method()` => this === obj***

***`function()` => this === window***





#### updating the state

```jsx
class Counter extends Component {
    state = {
        count: 0
    };

    constructor() {
        super();
        
        this.handleIncrement = this.handleIncrement.bind(this);
    }

    handleIncrement() {
		this.setState({count: this.state.count + 1}) //
    }

    render() {
		return(
        	<React.Fragment>
            	<button
                    onClick={this.handleIncfrement}
                    className="btn btn-secondary btn-sm"
				>
                    Increment
                </button>
            </React.Fragment>
        );
    }
}


```

***`this.setState({ count: this.state.count + 1 })`***





## 



#### pass data  

#### raise and handle events  

#### multiple components in sync  

#### functional components  

#### lifecycle hooks



### passing

```jsx
// counters.jsx

import React, { Component } from 'react';
import Counter from '.counter/';

class Counters extends Component {
    state = {
        counters: [
            { id: 1, value: 0 },
            { id: 2, value: 0 },
            { id: 3, value: 0 },
            { id: 4, value: 0 },
        ]
    };

    render() {
		return (
        	<div>
            	{this.state.counters.map(counter => (
                	<Counter key={counter.id} value={counter.value}>
                    	<h4>Counter #{counter.id}</h4>
                    </Counter>
                ))}
            </div>
        );
    }
}

export default Counters;

//-----

import React, { Component } from 'react';

class Counter extends Component {
    
    //---
    
    state = {
        value: this.props.value
    };

    handleIncrement = () => {
		thie.setState({count: this.state.value + 1})
    }
    
    //-----

    state = {
        value: this.props.value
    };

    constructor() {
		super();
        
        this.handleIncrement = this.handleIncrement.bind(this)
    }

    handleIncrement() {
		this.setState({count: this.state.value + 1})
    }

    //---

    render() {
        console.log('props', this.props);
        
        return (
        	<React.Fragment>
            	<h4>{this.props.children}</h4>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button
                    onClick={this.handleIncrement}
                    className="btn btn-secondary btn-sm"
                >
                    Increment
                </button>
            </React.Fragment>
        );
    }
}
```

