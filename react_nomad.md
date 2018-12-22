# React - Nomad



### session 1.

#### just JavaScript

- no framework to learn



#### Composition (구성)

- component (요소)별로  나눠서 볼 수 있음



#### unindirectional (단방향) dataflow

* Data is on the state
* The UI displays the data
* if the state changes, the UI updates
* Data -> UI
* ~~UI -> Data~~



***model / view / controller***





### session 3.

#### <u>webpack</u>

#### <u>create-react-app</u>

`create-react-app <폴더 이름>`





### session 5.

##### React와 ReactDOM의 차이점

##### React - UI(유저 인터페이스) 라이브러리

##### ReactDOM - 리액트를 웹사이트에 출력(render)하는 걸 도와주는 모델

=> React / ReactDOM 둘다 **라이브러리**

(DOM - Document Object Model)

리액트를 사용해서 웹사이트에 올려놓고 싶을 때는 **reactDOM**

리액트를 사용해서 모바일에 올려놓고 싶을 때는 **reactNative**



리액트 돔은 1개의 컴포넌트를 출력(render)

그 다큐먼트 안에 엘리먼트가 있는데, 엘리먼트 ID는 root

이건 인덱스 html파일에 숨겨져 있음



***컴포넌트는 무조건 render를 해주고 return 해야함.***

***render => return => JSX***



app.js에서 컴포넌트를 여러번 불러올 수 있음

**하지만 컴포넌트 각각의 id없이 마구 불러오는 것은 좋지 않음**





### session 6.

props / state

#### data flow with props

부모가 자식에게 정보를 주는 방법 => props

```js
// App.js

const movies = [
  "Matrix",
  "Full Metal Jacket",
  "oldboy",
  "Star Wars"
];

class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie title={ movies[0] } />
        <Movie title={ movies[1] } />
        <Movie title={ movies[2] } />
        <Movie title={ movies[3] } />
      </div>
    );
  }
}
```



```js
// Movie.js

class Movie extends Component {
  render(){
    console.log(this.props); // {title: "Matrix"}, ...
    return(
      <div>
        <h1>{ this.props.title }</h1>
        // "Matrix"
      </div>
    ) 
  }
}
```



`this.props` => `{title: "Matrix"}`

`this.props.title` => `"Matrix"`





### session 7.

#### <u>map</u>

```js
class App extends Component {
  render() {
    return (
      <div className="App">
        {movies.map(movie => {
          return <Movie title={movie.title} poster={movie.poster} />
        })}
      </div>
    );
  }
}
```





### session 8.

***React에서는 더 이상 PropTypes가 사용되지 않는다.***

`yarn add prop-types` 

PropTypes를 설치하면 사용할 수 있다.



```js
// Movie.js

import React, { Component } from 'react';
import PropTypes from 'prop-types';
import './Movie.css';

class Movie extends Component {

  // 이런 식으로 사용할 수 있다.
//----------------------------
  static propTypes = {
    title: PropTypes.string,
    poster: PropTypes.string
  }
//----------------------------

  render(){
    return(
      <div>
        <MoviePoster poster={ this.props.poster }/>
        {/* <h1>hello this is a movie</h1> */}
        <h1>{ this.props.title }</h1>
      </div>
    ) 
  }
}
```

PropTypes로 타입을 지정해 줄 수 있다

***TypeScript같은 느낌?***



`PropTypes.string` => 타입이 string이어야 한다.

`PropTypes.number` => 타입이 number여야 한다.



**<u>isRequired</u>**: prop을 제공하는 것이 필수로 설정!!!

ex) `PropTypes.string.isRequired`





### session 9.

#### ***life cycle***



***<u>WillMount => render => DidMount</u>***

순서를 숙지

WillMount는 사용(X)

```js
// app.js

class App extends Component {
  componentWillMount(){
    console.log('will mount');
  }
  componentDidMount(){
    console.log('did mount');
  }

  render() {
    console.log('render');
    return (
      <div className="App">
        {this.state.greeting}
        {movies.map((movie, index) => {
          console.log(index);
          return <Movie title={movie.title} poster={movie.poster} key={index} />
        })}
      </div>
    );
  }
}
```





### session 10.

#### ***state***

state는 리액트 컴포넌트 안에 있는 object

```js
// app.js

class App extends Component {

  state = {
    greeting: "Hello"
  }
  
  componentDidMount(){
    setTimeout(() => {
      this.setState({
        greeting: "Hello again!"
      })
    }, 2000);
  }

  render() {
    console.log('render');
    return (
      <div className="App">
        {this.state.greeting}
        {movies.map((movie, index) => {
          console.log(index);
          return <Movie title={movie.title} poster={movie.poster} key={index} />
        })}
      </div>
    );
  }
}
```

***state 변경은 setState로***





### session 11.

#### ***setState***

```js
// app.js

class App extends Component {
    
  state = {
    greeting: "Hello",
    movies: [
      {
        title: "Matrix",
        poster: "https://images-na.ssl-images-amazon.com/images/I/51FhdGyJ6DL.jpg"
      },
      {
        title: "Full Metal Jacket",
        poster: "https://i.pinimg.com/736x/36/1e/cd/361ecdb85a3767f70810cbe2cdaaf1a4.jpg"
      },
      {
        title: "oldboy",
        poster: "https://img.moviepostershop.com/oldboy-movie-poster-2003-1010420981.jpg"
      },
      {
        title: "Star Wars",
        poster: "https://images-na.ssl-images-amazon.com/images/I/81WjGytz7HL._SY445_.jpg"
      }
    ]
  }
  
  componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [
          ...this.state.movies, // 중요!!
          {
            title: "Trainspotting",
            poster: "https://i.pinimg.com/originals/88/66/65/886665e09c688e0bbb1fd7bc51c57671.jpg"
          }
        ]
      })
    }, 5000);
  }

  render() {
    console.log('render');
    return (
      <div className="App">
        {this.state.movies.map((movie, index) => {
          console.log(index);
          return <Movie title={movie.title} poster={movie.poster} key={index} />
        })}
      </div>
    );
  }
}
```

**`...this.state.movies`**

*이게 있고 없고의 차이*

***i) 있는 경우***

*=> 영화 리스트에 영화를 추가*

(이전 영화 리스트를 그대로 두고, 그리고 한 개 영화를 추가)



***ii) 없는 경우***

*=> 영화 리스트 전체를 대체*

(이전 영화 리스트를 전부 없애고 한 개의 영화만 표시)



참고) ***infinite scroll***

ex) instagram ...



**...this.state.movies`**의 위치를 바꿀 수도 있다!!

```js
// app.js

componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [
          {
            title: "Trainspotting",
            poster: "https://i.pinimg.com/originals/88/66/65/886665e09c688e0bbb1fd7bc51c57671.jpg"
          }
          ...this.state.movies, // 중요!!
        ]
      })
    }, 5000);
  }
```





### session 12.

#### ***loading states***



```js
// app.js

class App extends Component {

  state = {
  }
  
  componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [
          {
            title: "Matrix",
            poster: "https://images-na.ssl-images-amazon.com/images/I/51FhdGyJ6DL.jpg"
          },
          {
            title: "Full Metal Jacket",
            poster: "https://i.pinimg.com/736x/36/1e/cd/361ecdb85a3767f70810cbe2cdaaf1a4.jpg"
          },
          {
            title: "oldboy",
            poster: "https://img.moviepostershop.com/oldboy-movie-poster-2003-1010420981.jpg"
          },
          {
            title: "Star Wars",
            poster: "https://images-na.ssl-images-amazon.com/images/I/81WjGytz7HL._SY445_.jpg"
          },
          {
            title: "Trainspotting",
            poster: "https://i.pinimg.com/originals/88/66/65/886665e09c688e0bbb1fd7bc51c57671.jpg"
          },
        ]
      })
    }, 5000);
  }

  _renderMovies = () => { // 리액트 자체 기능이 많기 때문에 리액트 자체 기능과 나의 기능에 차이를 두기 위해서
    const movies = this.state.movies.map((movie, index) => {
      console.log(index);
      return <Movie title={movie.title} poster={movie.poster} key={index} />
    })
    return movies;
  }
  
  // state가 텅텅 비어있기 때문에
  render() {
    console.log('render');
    return (
      <div className="App">
        {this.state.movies ? this._renderMovies() : 'Loading'}
      </div>
    );
  }
}
```

`_renderMovies` 에서 `-` 를 사용하는 이유

=> 리액트 자체 기능이 많기 때문에 리액트 자체 기능과 나의 기능에 차이를 두기 위해서 ***(구분 짓기 위함)***



????? (이해 부족 해봐야 알듯?)

***state가 텅텅 비어있기 때문에***





### session 13. *

#### ***stateless functional component***

모든 component에 state가 있는 것은 아니다



* ***smart component => state(O)***

* ***dumb component => state(X) (props만 있음)***

  <u>***state(X) / function render(X) / life cycle(X)***</u>



????? (이해 조금)

function component는 클래스가 아니기 때문에

props가 필요없음?

```js
class MoviePoster extends Component {

  static propTypes = {
    poster: PropTypes.string.isRequired
  }

  render(){
    return(
      <img src={this.props.poster} />
    )
  }
}

// 위의 class를 
//-----
// 아래의 function으로 바꿔줄 수 있다.

function MoviePoster({poster}) {
  return (
    <img src={poster} alt="Movie Poster" />
  )
}

MoviePoster.propTypes = {
    poster: PropTypes.string.isRequired
}
```

=> 1개의 props만 있고, 1개의 html 태그만 필요

=> functional component밖에 없는 경우에는 



**`import React, {Component} from 'react';` 를**

**`import React from 'react';` 로 바꿔준다**

**`Component` 는 class component에서만 사용해주기 때문에**



**functional component에는 this가 필요없다.**

**이미 props를 쓰고 있기 때문에**





### session 14.

#### AJAX / JSON(JavaScript Object Notation)

***fetch*** => 뭔가를 잡는

```js
componentDidMount(){
    fetch("https://yts.am/api/v2/list_movies.json?sort_by=rating")
}
```



```js
componentDidMount(){
    console.log(fetch("https://yts.am/api/v2/list_movies.json?sort_by=rating"));
}
```

=> promise





### session 15.

#### ***promise***

