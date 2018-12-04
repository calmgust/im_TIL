# Server and Node



## Intro to Node

* An Overview of Node
* Node Modules and the CommonJS Pattern
* External Modules and npm
* Debugging Node





## An Overview if Node



***Node === JavaScript interpreter***



#### Blocking vs Non-Blocking

* **Blocking**: 커널(OS) 대기가 발생하면 기다림
* **Non-Blocking**: 대기가 필요할 경우 바로 종료



#### Sync vs Async

* **Sync**: 완료 시점을 응용 프로그램이 확인 **(능동적)**
* **Async**: 완료 시점에 이벤트가 발생. 일반적으로 callback을 통해 처리 **(수동적)**



=> 일반적으로 ***Sync + Blocking, Non-blocking, Asynchronous*** 3가지 상태가 존재



***Sync + Blocking***

***Non-blocking***

***Asynchronous (=> 비동기)***



#### The Node REPL (Read, Eval, Print, Loop)

```t
~ user$ node
> console.log('This is the Node REPL')
This is Node REPL
undefined
>
```



#### Running Applications with Node

` hello.js`

```javascript
// hello.js
console.log('GREETING, HUMAN');
console.log('YOU MAY ADDRESS ME AS NODE');
```

`Terminal`

```
~ user$ node hello.js
GREETING, HUMAN
YOU MAY ADDRESS ME AS NODE
~ user$
```



### Node.js 용도

* 웹 어플리케이션 서버
  * MEAN, MERN 등 *(A => 앵귤러 / R => 리액트)*
  * **Nginx + node.js** 조합으로 많이 사용됨
* REST API 서버
* 웹소켓을 이용한 프로젝트 (채팅 서버)
* 일반적인 프로그램





## Node Modules and the CommonJS Pattern



#### The CommonJS Pattern

* A contract for writing modular JavaScript (모듈형 자바스크립트 작성을 위한 계약)
* Each **module is created within its own file** with an isolated scope (각 **모듈**은 독립된 스코프로 **자체 파일 내에 생성**)
* The author of the module can **specify exactly what functionality needs to be exposed** (모듈 작성자는 **노출해야 하는 기능을 정확하게 지정**할 수 있다.)



#### Using Node modules

* `require()`

A method used to **import** another module's functionality into the focal module

* `module.exports`

An object used to **expose** parts of the focal module's functionality **to other modules**



`Authoring a module`

```javascript
// phone.js

var greeting = 'Ahoy-hoy';
var myNumber = '867-5309';

var answer = function () {
    console.log(greeting);
};

var dial = function (number) {
    console.log('calling ' + number);
};

module.exports = {
    myNumber: myNumber,
    answer: answer,
    dial: dial
}
```

`Using a module`

```javascript
// app.js

var telephone = require('./phone');

console.log(telephone.myNumber);
telephone.answer();
telephone.dial('634-5789');
```

![2018-11-19 16 21 22](https://user-images.githubusercontent.com/40155174/48691839-618f8a00-ec17-11e8-9b6d-bc42343e81eb.png)



![2018-11-19 16 25 46](https://user-images.githubusercontent.com/40155174/48691964-c77c1180-ec17-11e8-833c-64f3773218b6.png)





## External Modules and npm



### Loading External Libraries ( in the Browser )

`index.html`

```html
<html>
	<head>
        <title>Example</title>
        <script src="http://cdn.co/underscore.js"></script> <!--underscore를 사용하려면 script 코드 입력-->
        <script src="app.js"></script>
    </head>
    
    <body>
        ...
    </body>
</html>
```

`app.js`

```javascript
var school = ['Code States', 'Make School', 'Udacity'];

_.each(schools, function (school) { // => underscore 사용
    console.log(school + ' rules!');
});
```



### Loading External Libraries (in Node)

`app.js`

```javascript
// <script src="http://cdn.co/underscore.js"></script>
var _ = require('underscore'); // Node 환경일 경우

var school = ['Code States', 'Make School', 'Udacity'];

_.each(schools, function (school) { // => underscore 사용
    console.log(school + ' rules!');
});
```



#### Node's Core Modules

* Key functionality that comes bundles with Node
* Loaded via `require()`, like any other modules
* Includes:
  * `fs`
  * `http`
  * `url`
  * `path`
  * `and many more ...`

```javascript
const fs = require('fs');
const http = require('http');

fs.readFile('filename.json', (err, data) => {}); // read a file
http.get('http://nodejs.org/dist/index.json', (response) => {}); // request url using GET method
```



#### package.json

* package.json
  * 프로젝트의 의존성에 대해 명시한 파일
  * 필요한 패키지들의 버전 등에 대해 기술되어 있음
  * Task Runner로의 기능도 감당





## Debugging Node



### The Problem with `console.log()`

When you use `console.log()` in Node, it doesn't show up in the browser - it shows up in your terminal window.

![2018-11-19 16 46 40](https://user-images.githubusercontent.com/40155174/48692799-b1bc1b80-ec1a-11e8-855a-039ed1fb131c.png)



### A Better Way: `--inspect` flag

* It's like Chrome's Dev Tools, but for your server code
* Set breakpoints, watch, variables, and more
* Only works in Chrome
* See more: **Debugging Node.js with Chrome DevTools**







# Chatterbox Server

Chatterbox Server의 목표는 Chatterbox Client와 연동되는 서버를 만드는 것

Node.js를 이용하여

GET 요청이 들어왔을 때 메시지 목록을 돌려주고, POST 요청이 왔을 때 메시지를 쌓는 서버를 만드는 것

