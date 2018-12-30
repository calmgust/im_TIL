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

#### ***Transfiler or Transfomer***

#### <u>webpack</u>

=> 리액트 코드를 브라우저가 이해할 수 있는 코드로 변경해주는 역할

#### <u>create-react-app</u>

`create-react-app <폴더 이름>`





### session 5.

#### ***JSX***

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



<u>***부모 역할을 하는 컴포넌트 안에 자녀 역할을 하는 컴포넌트를 넣어준다.***</u>



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

#### ***life cycle (render / update)***



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

* componentWillMount

  => 사이클이 시작되는 것을 알 수 있음

* reder

  => 컴포넌트가 리액트 세계에 존재하게 되었음을 알 수 있음

* componentDidMount

  => 컴포넌트가 성공적으로 리액트 세계에 자리잡았음을 알 수 있음





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





### session 11. *

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

**`...this.state.movies`** (infinite scroll과 연관성)

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
      {/*this.state.movies가 있는 경우 render를 해주고 없는 경우에는 loading을 render해준다.*/}
    );
  }
}
```

`_renderMovies` 에서 `-` 를 사용하는 이유

=> 리액트 자체 기능이 많기 때문에 리액트 자체 기능과 나의 기능에 차이를 두기 위해서 ***(구분 짓기 위함)***



????? (이해 부족 해봐야 알듯?)

***state가 텅텅 비어있기 때문에***



*render function에서* 

this.state.movies가 있는 경우에는 this.state.movies를 render 해준다. 

*this.state.movies가 없는 경우에는 loading을 render 해준다.*





### session 13. *

#### ***stateless functional component***

모든 component에 state가 있는 것은 아니다



* ***smart component => state(O)***

* ***dumb component => state(X) (props만 있음)***

  <u>***state(X) / function render(X) / life cycle(X)***</u>



????? (이해 조금)

function component는 클래스가 아니기 때문에

this.props가 필요없음?

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

function MoviePoster({poster}) { // {poster} 여기도 주의!!
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



##### class(smart)를 functional(dumb)로 바꿀 때

* ***`{poster}` => parameter 주의***

* `this.props.poster` => `poster`

  => ***class가 아니기 때문에  this.props가 필요없다***

* functional은 단순히 return을 하기 위해 존재



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





### session 15. *

#### ***promise***

```js
componentDidMount(){
    console.log(fetch("https://yts.am/api/v2/list_movies.json?sort_by=rating"));
    console.log('hello');
}
```

두번째 라인 hello는 첫번째 라인 fetch가 끝나지 않으면 실행되지 않는다.

=> ***synchronous(동기)***



```js
componentDidMount(){
    console.log(fetch("movie_api"));
    console.log(fetch("anime_api"));
}
```

만약 영화 서버가 느리면 애니메이션은 계속 기다려야 한다. 비록 애니메이션 서버가 영화 서버보다 빠를지라도 (동기적이기 때문에)

=> ***이러한 경우 promise를 사용***

***promise는 asynchronous(비동기)***

1. 첫 번째 라인이 다 끝나든 말든, 두 번째 라인이 작업을 한다는 의미

   => 계속 다른 작업을 스케쥴해놓을 수 있다. (장점)

2. 시나리오 잡는 방법을 만들어 준다

***fetch, promise가 좋은 이유는 시나리오가 생기고 이를 관리할 수 있다***



```js
componentDidMount(){
    fetch("movie_api")
    .then(response => console.log(response))
    .catch(err => console.log(err))
}
```

***=> `fetch()` 작업이 완료되면 `.then()` 을 실행해라***

=> `.then()`function은 1개의 ***attribute(object)***만을 준다

fetch의 결과물은 response

```js
componentDidMount(){
    fetch("movie_api")
    .then(response => response.json())
    .then(json => console.log(json))
    .catch(err => console.log(err))
}
```





### session 16. **

#### ***Async / Await***

***callback hell에 빠지지 않기 위해서***

ex) .then .then .then ....



```js
class App extends Component {

  state = {}

  // componentDidMount(){
  //   fetch("https://yts.am/api/v2/list_movies.json?sort_by=like_count")
  //   // .then(response => console.log(response))
  //   .then(response => response.json())
  //   .then(json => console.log(json))
  //   .catch(err => console.log(err))
  // }

  componentDidMount(){
    this._getMovies();
  }

  _renderMovies = () => {
    const movies = this.state.movies.map((movie, index) => {
      console.log(index);
      return <Movie title={movie.title} poster={movie.large_cover_image} key={index} />
    })
    return movies;
  }

  _getMovies = async () => {
    const movies = await this._callApi() // _callApi가 끝나기를 기다림
    this.setState({ // _callApi가 끝나고 나서 실행
      movies // _callApi의 return value
    })
  }

  _callApi = () => {
    return fetch("https://yts.am/api/v2/list_movies.json?sort_by=like_count") // fetch를 return 해줘야
    .then(response => response.json())
    .then(json => json.data.movies)
    .catch(err => console.log(err))
  }

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

1. fetch를 `_callApi()` 로 변경
2. `_getMovies()`라는 function을
3. `_getMovies()` 는 asynchronous function(***async***)
4. `_callApi()` 작업이 완료되고 return하기를 ***await***
5. `_callApi` 는 fetch promise를 return할 것인데 이는 모든 데이터는 JSON이라 `json.data.movies`
6. `json.data.movies` 라는 value는, const movies의 결과값
7. component의 state를 movies로 set



component의 key는 인덱스로 사용하는 것이 좋지 않다!

=> 느려진다





### session 17. **

***JSX에서는 class를 className이라고 해줘야 한다***

줄 세우기?



### session 18.

#### ***CSS***

***LineEllipsis => ...***

글을 줄이고 요약해서 render해서 보여준다

```js
import LinesEllipsis from 'react-lines-ellipsis'
 
<LinesEllipsis
  text='long long text'
  maxLine='3'
  ellipsis='...'
  trimRight
  basedOn='letters'
/>
```

***구글에서 LineEllipsis라고 검색***





### session 19.

#### ***deploy / github***

***yarn build***

localhost에 있을 때 사용하는 코드는 압축되어있지 않고, 느리고, 최적화되어 있지 않는데 ***build*** 를 하는 경우에는 압축되고, 빨라지고, 최적화되어 성능이 더욱 향상된다.