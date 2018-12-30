# React - Udemy



## section 1.



### 1. 프로젝트 파일과 관련된 github와 link 소개

##### Question.

Email: ste.grider@gmail.com

Twitter: @sg_in_sf

Github: GitHub.com/stephengrider





### 2. github

Github 주소

https://github.com/StephenGrider/ReduxCasts





### 3. 보일러 플레이트(Boilerplate) 프로젝트의 목적

* **보일러 플레이트 (boiler plate)**

  재사용 가능하고 적은 수정만으로 여러 곳에 활용 가능한 소스코드



ES6의 모든 기능을 완전히 지원하는 브라우저가 없기 때문에 

**툴링(Tooling)** 혹은 **트랜스파일(Transpile)**하는 과정이 필요

트랜스파일을 하기 위해서 **웹팩(webpack)**이라 불리는 도구를 이용

**바벨(Babel)** 혹은 **바벨JS(Babel.js)**라고 불리는 라이브러리로 구성할 것

***=> 웹팩과 바벨의 목적은 ES6 코드가 바로 브라우저에서 실행하지 못하는 문제를 해결하기 위함***

이러한 과정을 거칠 경우 하나의 파일이 생성





### 4. 개발환경 설정

보일러 플레이트 어플리케이션 설치

`npm install`





### 5. 프로젝트 설정

`npm start`

localhost:8080





### 6. JSX와의 첫 만남

리액트(React)는 **웹브라우저에 보여지는 HTML을 만드는** 자바스크립트 라이브러리

```js
//index.js


// Create a new component, This component should produce some HTML
// 새로운 컴포넌트를 생성, 이 컴포넌트는 HTML을 생성하게 될 것

// const로 선언한 변수는 무조건 최종값을 갖는다. (선언 이후 변하지 않는다. = 선언된 이후 재할당 되지 않는다.)
// constant(상수): 변하지 않는 값 / variable(변수): 변하는 값
const App = function () {
  return <div>Hi!</div>;
}

// 리액트야 내가 만든 컴포넌트를 DOM으로 넣어죠
// Take this component's generated HTML and
// 이 컴포넌트가 만든 HTML을 가져오고
// put it on the page (in the DOM)
// 페이지에 반영한다
```





### 7. JSX를 더 파보자

웹팩과 바벨같은 보일러플레이트 패키지의 목적

***=> JSX를 바닐라 자바스크립트로 변환하여 브라우저가 이해할 수 있게 만든다는 점***

***=> JSX의 목적은 자바스크립트 코드를 궁극적으로 HTML으로 만들기 위한 것***



* **바닐라 자바스크립트**

  프레임워크나 라이브러리 없이 순수한 자바스크립트



Babel(babeljs.io/repl)에서 확인





### 8. ES6 불러오기(import)구문

```js
import React from 'react';


React.render(App);
```





### 9. 리액트DOM vs 리액트

```js
import React from 'react';
import ReactDOM from 'react-dom';


ReactDOM.render(App);
```





### 10. 컴포넌트 인스턴스와 컴포넌트 클래스의 차이

```js
ReactDOM.render(<App />);
 // 이 코드는 이제 App의 인스턴스를 생성하고 이를 ReactDOM.render에 전달
```





### 11. 타겟 렌더링(target rendering)

```js
ReactDOM.render(<App />, document.querySelector('.container'));
// <App />의 인스턴스를 .container 클래스에서 렌더링
```

***container라는 클래스를 가진 div를 찾고, 이 div에 app 컴포넌트를 렌더링하라는 말***



### 12. 컴포넌트의 구조

<img width="635" alt="2018-12-05 16 24 37" src="https://user-images.githubusercontent.com/40155174/49496875-53de3380-f8aa-11e8-9e03-c010832a08bd.png">

*여러 개의 컴포넌트로 분리하는 경우*

가능한 **기능적인 부분을 독립**시킬 수 있음

이렇게 작은 컴포넌트를 만들면 애플리케이션을 만들 떄 **코드를 쉽게 재사용**할 수 있음



***각 파일당 하나의 컴포넌트를 만들어야***





### 13. 유튜브(Youtube) 검색 API 회원가입

https://console.developers.google.com

키 생성 후

디렉터리 안에서 `npm install --save youtube-api-search` 을 실행하여 설치

***=> `--save` 라는 명령어는 package.json 파일에 자동으로 저장해달라는 의미***

package.json 파일 내에서 

***devDependencies / dependencies => 설치되어 있는 보일러플레이트 어플리케이션을 확인할 수 있다.***





### 14. 내보내기(export) 구문

***export module / class / state*** 세 가지 중요한 개념

```js
import React from 'react';

const SearchBar = () => { // <SearchBar /> Component
  return <input /> // React.createElement
};

export default SearchBar;
// SearchBar를 내보내겠다 (import 하는 곳으로)
```

***import / export module 추가 공부 필요***





### 15. 클래스 기반의 컴포넌트

```js
// functional
const SearchBar = () => {
    return <input />;
};
    

// class
import React from 'react';

class SearchBar extends React.Component {
    render() {
        return <input />;
    }
}

//-----

import React, { Component } from 'react';
// const Component = React.Component;

class SearchBar extends Component {
    render() {
        return <input />;
    }
}

```





### 16. 유저 이벤트 핸들링(user event handling) *

리액트에서 이벤트를 핸들링할 때는 두 가지 과정 필요

1. **이벤트 핸들러 선언**

   *이 이벤트 핸들러는 이벤트가 발생할 때마다 실행되는 함수*

2. **이벤트 핸들러를 살펴보려는 요소에 전달**

   이 경우에 검색바 안의 인풋 요소의 텍스트가 바뀌는 것을 알려고 하는 것

```js
// class 밖에 함수를 설정해주는 경우 (속도가 더 빠르다!)

class SearchBar extends React.Component {
    render() {
        return <input onChange={this.onInputChange} />; // *
    }
    
    onInputChange(event) { // 패러미터 event는 꼭 event가 아니어도 된다. ex) e
    console.log(event.target.value); // *
	} // input 창에 입력한 값이 console에 찍힌다.
}


//-----

// input 태그 안에 함수를 설정해주는 경우 (보기에는 편하지만 속도가 느리다!)

class SearchBar extends React.Component {
    render() {
        return <input onChange={event => console.log(event.target.value)} />
    }
}
```

***`event.target.value`***





### 17. 상태 (state) 소개

* **state**

  스테이트(state)는 자바스크립트 객체로 ***유저 이벤트를 저장하고 반응하는데 이용***

  컴포넌트 기반의 ***각 클래스는 그 자체의 스테이트 객체를 가진다.***

  *컴포넌트 스테이트가 바뀔 때마다*, 컴포넌트는 즉시 리렌더링(***render함수가 재실행***)하고 자식 요소들에게도 렌더링하도록 강제한다.



  함수형(functional) 컴포넌트는 스테이트를 가지지 않습니다.

  클래스(class) 기반의 컴포넌트만 스테이트를 가질 수 있습니다.

```js
class SearchBar extends React.Component {
     // SearchBar 컴포넌트가 Component를 상속받는데
 	 // Component에는 constructor 함수를 가진다.
    constructor(props) {
        // constructor 함수는 클래스 안에서 뭔가를 설정하는데 활용
    	// 변수나 상태값을 초기화하는 등에 주로 이용
        super(props);
        // super를 호출하는 경우 부모 class의 메소드를 호출할 수 있다.
        
        
        // state를 사용할 때마다 새로운 object를 생성하면서 초기화를 하게 됩니다.
    	// 그리고 this.state에 할당
        this.state = {
            term: ''
        };
        // 유저가 검색 input에 업데이트를 할 때마다
	    // this.state.term이 업데이트 되거나 변경 사항을 받아 옵니다.
   		// 유저가 입력창 안에 타이핑을 하기 시작하면 
    	// this.state.term 부분이 빈 문자열이 아닌 입력값을 갖게 될 것
    }
    
    render() {
        return <input onChange={event => console.log(event.target.value)} />;
    }
}
```





### 18. 상태 (state) 더 파고들기 *

```js
class SearchBar extends React.Component {
  constructor(props) { 
    super(props);

    this.state = {
      term: ''
    };
  }

  render() {
    return <input onChange={event => this.setState({ term: event.target.value })} />
	// this.setState({})
  }
}
```

**`this.state = {}` 의 변경은 `this.state`가 아니라 `this.setState({})` 로 변경을 해주어야 한다.**



```js
class SearchBar extends React.Component {
  constructor(props) { 
    super(props);

    this.state = {
      term: ''
    };
  }

  /*
  render() {
    return <input onChange={event => {
      console.log(event.target.value);
      return this.setState({ term: event.target.value })
    }} />
  */

  render() {
    return (
      <div>
        <input onChange={event => this.setState({ term: event.target.value })} />
        Value of the input: {this.state.term} {/* term값을 수정하는 것이 아니라 참조하기 위한 조치 */}
      </div>
    );
  }
}
```

***tip. 글자 수 카운트***





### 19. <u>제어 컴포넌트</u> ***

#### (추가 학습 필요 => 스테이트에서 가장 혼란스러운 부분)

```js
class SearchBar extends React.Component {
  constructor(props) { 
    super(props);

    this.state = {
      term: ''
    };
  }

  render() {
    return (
      <div>
        <input 
          value = {this.state.term} // (밑에 onChange를 삭제하면)값이 입력되지 않는다!!
    	  onChange={event => this.setState({ term: event.target.value })} // 새로운 변화의 값이 있다는 것을 알려준다
        />
      </div>
    );
  }
}
```





### 20. 짧은 휴식 그리고 리뷰

* JSX
* Component
* State
* ES6 (class / arrow function / import / export / API)



* functional / class Component





---



## section 2.

### 리액트와 비동기 리퀘스트(Ajax Requests)



### 21. 유튜브(Youtube) 검색 반환

* ***하향 데이터 플로우 : 모든 <u>부모 컴포넌트는 데이터를 가져올 권리를 가져야</u> 한다.***

```js
import React from 'react';
import ReactDOM from 'react-dom';
// 다운로드를 위한 검색 패키지를 접근하기위해 이를 불러오는 것이 필요
import YTSearch from 'youtube-api-search';

import SearchBar from './components/search_bar';

const API_KEY = 'asfdkajsfljasd';
YTSearch({key: API_KEY, term: 'surfboards'}, function(data) {
    console.log(data);
})

// 부모 컴포넌트
// 데이터를 가져오는 것을 전담하는 컴포넌트
const App () => {
    return (
    	<div>
        	<SearchBar />
    	</div>
    );
}

ReactDOM.render(<App />, document.querySelector('.constainer'));
```





### 22. 함수형 컴포넌트를 클래스 컴포넌트로 리펙토링하기(refactoring)

```js
const App () => {
    return (
    	<div>
        	<SearchBar />
        </div>
    );
}


// refactoring

class App extends React.Component { 
// class App extends Component
    render() {
        return (
        	<div>
            	<SearchBar />
            </div>
        );
    }
}
```



```js
class App extends React.Component { 
// class App extends Component
    constructor(props) {
        super(props);
        
        this.state = { videos: [] };
        
        YTSearch({key: API_KEY, term: 'surfboards'}, videos => {
            this.setState({ videos }); // ES6 => key와 value가 같을 경우에? key와 변수의 이름이 같은 경우에?
            // this.setState({ videos: videos })
            // 문법에 익숙해지자
        })
    }
    
    render() {
        return (
        	<div>
            	<SearchBar />
            </div>
        );
    }
}
```





### 23. props

```js
// video_list.js


import React from 'react';

// 두 개(index.js / search_bar.js?)의 상위 비디오 리스트 컴포넌트를 가지고 시작
// 이들은 스테이트가 필요하지 않습니다.
// 유저 인터렉션을 감지하지 않아도 되고, 어떤 형태로 리렌더링 되지 않아도 된다.
// 그래서 단순한 함수형 컴포넌트를 만들 것

const VideoList = () => {
  return (
    <ul className="col-md-4 list-group"> {/* 부트스트랩 컬럼 설정 */}
		{props.videos.length}
    </ul>
  );
};

export default VideoList;
```



```js
// index.js

import React from 'react';
import ReactDOM from 'react-dom';
import YTSearch from 'youtube-api-search';

import SearchBar from './components/search_bar';
// video-list를 export했으니 import해와야
import VideoList from "./components/video_list";

const API_KEY = 'asdf';


class App extends Component {
  constructor(props) {
    super(props);

    this.state = { videos: [] };

    YTSearch({key: API_KEY, term: 'surfboards'}, videos => {
      this.setState({ videos });
    });
  }

  render() {
    return (
      <div>
        <SearchBar />
        <VideoList videos={this.state.videos}/> // div에 넣어준다!!
      </div>
    );
  }
}


ReactDOM.render(<App />, document.querySelector('.container'));
```

***부모 컴포넌트 `<App / >`에서 자식 컴포넌트 `<VideoList />` 로 데이터를 전달해야 한다.***

#### 함수형(functional) 기반 컴포넌트를 클래스(class) 기반 컴포넌트로 리펙토링할 때 알아야할 중요한 것은 <u>*props를 this.props로 바꿔야*</u> 한다는 점

* ***functional (props)***
* ***class (this.props)***





### 24. Map으로 리스트 만들기

```js
var arr = [1,2,3];

arr.map(function(num) {return num*2});
arr.map((num) => { return num * 2});
arr.map(map => num * 2);
// [2,4,6]

arr.map(function(num) {return `<div>${num}</div>`})
// ["<div>1</div>", "<div>2</div>", "<div>3</div>"]
```



```js
// video_list.js

import React from 'react';
import VideoListItem from './video_list_item';

const VideoList = (props) => {
    const videoItems = props.videos.map(video => {
        return <VideoListItem video={video} />
    });
    
    return (
    	<ul className="col-md-4 list-group"> {/*부트스트랩 컬럼 설정*/}		{videoItems}
        </ul>
    );
}

export default VideoList;
```



```js
// video_list_item.js

import React from 'react';

const VideoListItem = (props) => {
    return <li>Video</li>
};

export default VideoListItem;
```





### 25. <u>리스트 아이템 키</u>(list item key)*

#### (추가 학습 필요 => 이해 부족)

```js
// video_list.js

import React from 'react';
import VideoListItem from './video_list_item';

const VideoList = (props) => {
    const videoItems = props.videos.map(video => {
        return <VideoListItem key={video.etag} video={video} 				/>
        // 배열의 각 자식은 특별한 key prop를 가져야 한다.
    	// 각 리스트 아이템에 키를 넣어서 리액트가 빠른 방법으로 적절한 레코드를 업데이트할 수 있다는 것을 확인
    	// 언제나 키를 추가하는 것을 확인하는 것은 좋은 자세
    });
    
    return (
    	<ul className="col-md-4 list-group"> {/*부트스트랩 컬럼 설정*/}		{videoItems}
        </ul>
    );
}

export default VideoList;
```

Warning: Each child in an array or iterator should have a unique "key" prop.

Check the render method of 'VideoList'.

***=> 이 배열의 각 자식은 특별한 key prop을 가져야 한다***

배열 아이템들을 렌더링할 때마다, 리액트는 리스트를 만드는 것이라 가정

***각 리스트 아이템에 키를 넣어서 리액트가 빠른 방법으로 적절한 레코드를 업데이트할 수 있다는 것을 확인***

성능이 증가?

**언제나 키를 추가하는 것을 확인하는 것은 좋은 자세**





### 26. <u>비디오 리스트 아이템</u>(video list item)**

***비디오 리스트를 현재 보다 보기 좋게 만드는 것에 초점***

```js
// video_list_item.js


import React from 'react';

// const VideoListItem = (props) => {
//   const video = props.video;

//   return <li>Video</li>
// };

const VideoListItem = ({ video }) => {
  // const video = props.video; 위에 { video }는 같은 것
  // console.log(video); 각 비디오 아이템에 대한 콘솔 로그를 얻게됨
  // 주의를 기울여야할 유일한 프로퍼티는 snippet object
  const imageUrl = video.snippet.thumbnails.default.url;

  // list태그 안에 div태그로 정리
  return (
    <li className="list-group-item">

      <div className="video-list media">
        <div className="media-left">
          <img className="media-object" src={imageUrl} />
        </div>

        <div className="media-body">
          <div className="media-heading">{video.snippet.title}</div>
        </div>
      </div>

    </li>
  );
};


export default VideoListItem;
```





### 27. 디테일 컴포넌트와 템플릿 문자열

***`video_detail.js` 에 컴포넌트는 유저가 실제로 선택한 비디오를 볼 수 있고 플레이 하도록*** 

**새로운 컴포넌트를 작성하기 전에 자신에게 물어봐야할 질문**

**=> 컴포넌트가 어떤 스테이트든 유지할 필요가 있느냐?**

비디오 플레이 할 때 여기서는 유튜브 임베드를 사용할 것

실제로 비디오 디테일은 비디오 타이틀과 내용과 url을 신경 쓸 필요가 있음

여기에는 app 컴포넌트로부터 내려오고 props를 통해 이용가능한 모든 프로퍼티들이 있음

*<u>이 비디오 디테일에는 어떤 스테이트도 필요하지 않음</u>*

**=> 단순한 함수형(functional) 컴포넌트만 필요**

```js
// video_detail.js


import React from 'react';

const VideoDetail = ({video}) => {
  // const video = props.video; 위에 {video}와 같다.
  const videoId = video.id.videoId;
  const url = `https://youtube.com/embed/${videoId}`; // 템플릿 문자열

  return (
    <div className="video-detail col-md-8">

      <div className="embed-responsive embed-responsive-16by9">
        <iframe className="embed-responsive-item" src={url}></iframe>
      </div>

      <div className="details">
        <div>{video.snippet.title}</div>
        <div>{video.snippet.description}</div>
      </div>

    </div>
  );
};

export default VideoDetail;
```





### 28. 널(null) props 핸들링하기

```js
// index.js


import React from 'react';
import ReactDOM from 'react-dom';

import VideoDetail from './components/video_detail';


class App extends React.Component {
    constructor(props) {
        super(props);
        
        this.state = {
            videos: []
        }
        
        YTSearch(...);
    }
    
    render() {
        return(
        	<div>
            	...
            	<VideoDetail video={this.state.videos[0]} />
				{/* Cannot read property 'id' of undefined */}
				...
            </div>
        );
    }
}

ReactDOM.render(<App />, document.querySelector('.container'));
```



```js
// video_detail.js


import React from 'react';

const VideoDetail = ({video}) => {
  // const video = props.video; 위에 {video}와 같다.

    
  // video를 호출하려고 하면, undefined의 프로퍼티 아이디를 읽을 수 없다는 에러
  // video.id를 읽으려고 해도 video가 undefined 이기에 아무것도 없는 것

  // 리액트는 즉시 렌더링하길 원하고 기다리지 않음
  // 어떤 부모 객체는 자식 객체의 필요를 만족시키도록 빠르게 정보를 가져올 수 없음
  // 이 경우에는 비디오 디테일 컴포넌트 안에 체크 사항을 추가
  // 렌더링을 시도하기 전에 비디오가 props에 주어졌는지 확인하는 과정
  if (!video) {
    return <div>Loading...</div>
    // 비디오 디테일을 렌더링할 때 비디오가 제공되지 않으면, 이 떄 loading이 반환되는데
    // 이 때 다른 나머지 프로세스는 위에서 return을 해주기 때문에 실행되지 않는다.
  }

  const videoId = video.id.videoId;
  const url = `https://youtube.com/embed/${videoId}`; // 템플릿 문자열

  return (
    <div className="video-detail col-md-8">

      <div className="embed-responsive embed-responsive-16by9">
        <iframe className="embed-responsive-item" src={url}></iframe>
      </div>

      <div className="details">
        <div>{video.snippet.title}</div>
        <div>{video.snippet.description}</div>
      </div>

    </div>
  );
};

export default VideoDetail;
```

리액트는 즉시 렌더링하길 원하고 기다리지 않는다. 그렇기 때문에 어떤 부모 객체는 자식 객체의 필요를 만족시키도록 빠르게 정보를 가져올 수 없다.

이 경우에는 자식 컴포넌트 안에 체크 사항을 추가하여야 한다.( if 문 / 렌더링을 시도하기 전에 props가 주어졌는지 확인하는 과정 )

렌더링할 때 비디오가 제공되지 않으면, 이 때 loading이 return되는데, 이 때 다른 나머지 프로세스는 위에서 return을 해주었기 때문에 실행되지 않는다.





### 29. <u>비디오 선택</u>(video select)*

#### (난이도)

```js
// index.js


import React from 'react';
import ReactDOM from 'react-dom';
import YTSearch from 'youtube-api-search';

import SearchBar from './components/search_bar';
import VideoList from "./components/video_list";
import VideoDetail from "./components/video_detail";

const API_KEY = 'AIzaSyAuuKBZkuvRGEpLvQOQqu8Cr9sJwdDASoU';


class App extends Component {
  constructor(props) {
    super(props);

    this.state = { 
      videos: [],
      selectedVideo: null // 비디오를 선택하기 위함
    };

    YTSearch({key: API_KEY, term: 'BTS'}, videos => {
      this.setState({
        videos: videos,
        selectedVideo: videos[0] // 초기값 설정
      });
    });
      
  }

  render() {
    return (
      <div>
        
		<SearchBar />
        <VideoDetail video={this.state.selectedVideo} />

        <VideoList 
			onVideoSelect={selectedVideo => this.setState({selectedVideo}) {/* callback 함수를 만들어 준다 */}
			videos={this.state.videos} />
                
      </div>
    );
  }
}


ReactDOM.render(<App />, document.querySelector('.container'));
```



```js
// video_list.js


const VideoList = (props) => {
  // const videos = props.videos;

  const videoItems = props.videos.map(video => {
    return (
      <VideoListItem
        onVideoSelect={props.onVideoSelect} {/* index.js에서의 callback funtion을 받아옴 */}
        key={video.etag} 
        video={video} />
    );

  });
```



```js
// video_list_item.js


const VideoListItem = ({ video, onVideoSelect }) => {
  // const video = props.video;
  // const onVideoSelect = props.onVideoSelect; 위에 { video, onVideoSelect }와  같은 것
  // onVideoSelect => callback function

    
  const imageUrl = video.snippet.thumbnails.default.url;

  return (
    <li onClick={() => onVideoSelect(video)} className="list-group-item">
	{/* onClick event안에서 callback function을 실행 */}
      
      
      <div className="video-list media">
        <div className="media-left">
          <img className="media-object" src={imageUrl} />
        </div>

        <div className="media-body">
          <div className="media-heading">{video.snippet.title}</div>
        </div>
      </div>

    </li>
  );
};
```

위의 callback은 **부모 컴포넌트로부터 자식 컴포넌트로 전달**

이렇게 두 레벨(두 단계) 이상으로 넘어가는 것은 약간 드문 경우

***(=> 두 개의 컴포넌트를 거치는 경우)***

<u>callback을 전달하는 것은 부모 컴포넌트와 자식 컴포넌트가 소통하기 위한 훌륭한 방법</u>





### 30. CSS로 스타일링(styling)

#### CSS tip.

***각 컴포넌트에서 상위 태그에 className을 컴포넌트 이름과 맞추어 주는 것***

***=> 클래스 이름을 컴포넌트 이름과 일치시키기***

<u>각 컴포넌트마다 연결된 CSS파일 하나를 찾을 수 있다.</u>

```js
// search-bar.js


class SearchBar extends React.Component {
    constructor(props) {
        super(props);
        
        this.state = {
            term: ''
        };
    }
    
    render() {
        return(
        	<div className="search-bar"> 
            {/* 상위 태그에 className을 컴포넌트 이름과 맞추어 주는 것 */}
            	<input 
            		value = {this.state.term}
    				onChange={event => this.setState({term: event.target.value})} />
            </div>
        );
    }
}
```



```css
.search-bar {
  margin: 20px;
  text-align: center;
}

/* search-bar와 그 자식인 input */
.search-bar input {
  width: 75%;
}

/* video-item과 img셀렉터(썸네일) */
.video-item img {
  max-width: 64px;
}

.video-detail .details {
  margin-top: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

/* 유저가 해당 것에 마우스 오버 했을 경우 
클릭 할 수 있다고 느낄 수 있다. */
.list-group-item {
  cursor: pointer;
}

/* 마우스 오버 시에 
pseudo 셀렉터인 hover를 사용하여 
배경색 변경(배경색 강조) */
.list-group-item:hover {
  background-color: #eee;
}

```





### 31. 비디오 검색(video searching) *

***상단에 SearchBar를 연결***

#### ***토픽 검색에 사용 가능*** *

```js
// index.js


import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import YTSearch from 'youtube-api-search';

import SearchBar from './components/search_bar';
import VideoList from "./components/video_list";
import VideoDetail from "./components/video_detail";

const API_KEY = 'AIzaSyAuuKBZkuvRGEpLvQOQqu8Cr9sJwdDASoU';


class App extends Component {
    constructor(props) {
        super(props);
        
        this.state = {
            videos: [],
            selectedVideo: null // 비디오를 선택하기 위함
        };
        
        this.videoSearch('BTS');
        // 해당 term을 넘기는 형태로
    }
    
    // 새로운 method를 만들어준다
    videoSearch(term) {
        // constructor 안에 있던 YTSearch() 함수를 새로 만든 videoSearch() 함수 안으로 이동
        YTSearch({key: API_KEY, term: term}, videos => {
            this.setState({
                videos: videos,
                searchedVideo: videos[0] // 초기값 설정
            });
        });
    }
    
    render() {
        return(
        	<div>
            	<SearchBar onSearchTermChange={term => this.videoSearch(term)}/>
            	<VideoDetail video={this.state.selectedVideo}/>
            	<VideoList 
					onVideoSelect={selectedVideo => this.setState({selectedVideo})}
                    videos={this.state.videos}/>
            </div>
        );
    }
}
    
ReactDOM.render(<App />, document.querySelector('.container'));
```



```js
// search_bar.js


import React from 'react';


class SearchBar extends React.Component {
    constructor(props) {
        super(props);
        
        this.state = {
          term: ''  
        };
    }
    
    render() {
        return(
        	<div className="search_bar">
            	<input 
            	value={this.state.term}
    
    			onChange={event => this.onInputChange(event.target.value)}
                // 검색을 하기 위해서 onInputChange 함수 안에 event.target.value를 인자로 넣어준다.
                />
            </div>
        );
    }
    
    
    // 위의 input 태그 안에 callback을 넣을 경우 복잡해질 수 있기 때문에
    // 이벤트 핸들러를 분리하여 새로운 method를 만들어 준다.
    onInputChange(term) {
        // 두 가지 목적
        this.setState({term});
        // 1. setState를 하는 것
        this.props.onSearchTermChange(term);
        // 2. onSearchTermChange callback function invocation
    }
}

export default SearchBar;
```





### 32. 인풋(input) 검색어 조절 *

**검색 주기를 조절 (유저가 타이핑을 시작할때 어느정도 시차를 두고 제시)**

***=> 이 조절을 위해 lodash라 불리는 함수 라이브러리를 이용***

이 라이브러리는 많은 유틸리티 메소드가 있는데, 그 중 하나가 **debounce**

***=> debounce는 함수의 호출 시기를 조절 가능***

**`npm install --save lodash`**

```js
// index.js


import _ from 'lodash';

import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import YTSearch from 'youtube-api-search';

import SearchBar from './components/search_bar';
import VideoList from "./components/video_list";
import VideoDetail from "./components/video_detail";

const API_KEY = 'AIzaSyAuuKBZkuvRGEpLvQOQqu8Cr9sJwdDASoU';


class App extends React.Component {
    constructor(props) {
        super(props);
        
        this.state = {
            videos: [],
            selectedVideos: null
        };
        
        this.videoSearch('BTS');
    }
    
    
	videoSearch(term) {
    	YTSearch({key: API_KEY, term: term}, videos => {
            this.setState({
                videos: videos,
                selectedVideo: videos[0]
      		});
    	});
  	}
    
    
    render() {
        
        // 기존 함수인 onSearchTermChange가 새로운 검색어로 videoSearch를 호출하고 전달
    	// onSearchTermChange 함수를 몇 초마다 호출할 계획
        const videoSearch = _.debounce(term => { this.videoSearch(term) }, 300)
        
        return(
        	<div>
            	{/* 이를 가지고 반환하는 함수는 0.3초마다 호출 */}
            	<SearchBar onSearchTermChange={videoSearch}/>
				...
            </div>
        );
    }
}

ReactDOM.render(<App />, document.querySelector('.container'));
```





### 33. 리엑트 마무리



