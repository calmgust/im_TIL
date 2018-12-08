# express



## 1. express-generatgor

package.json을 만들어주고 기본 폴더 구조까지 잡아주는 패키지

(express-generator)는 콘솔 명령어이므로 npm 전역 설치가 필요

`npm i -g express-generator`



설치 완료 후 새 익스프레스 프로젝트 생성

`express <프로젝트 이름>`

`cd <프로젝트 이름>`

`npm install` or `yarn add`?

`npm start` or `yarn start`?





http://localhost:3000 으로 접속하면

Express

Wlocome to Express 페이지가 출력



http://localhost:3000/users 에 접속하는 경우

respond with a resource



---

***익스프레스 초기 폴더 구조***

* bin
  * www <서버를 실행하는 스크립트>
* node_module
* public <외부(브라우저 등 의 클라이언트)에서 접근>
  * images
  * javascripts
  * stylesheets
    * style.css
* routes <주소별 라우터들을 모아둔 곳> => 서버의 로직은 모두 routes 폴더 안의 파일에 작성
  * index.js
  * users.js
* views <템플릿 파일들을 모아둔 곳> => 화면 부분은 모두 views 폴더 안에 작성
  * error.pug / error.jade
  * index.pug / index.jsde
  * layout.pug / layout.jade
* models <데이터 부분을 작성하는 곳>
* app.js
* package-lock.json
* package.json

---



bin/www 파일은 http 모듈에 express 모듈을 연결하고, 포트를 지정하는 부분

( www파일은 js확장자가 없다 )



* ***www***

```js
#!/usr/bin/env node
// 파일을 콘솔 명령어로 만들 수 있다.

/**
 * Module dependencies.
 */

var app = require('../app');
var debug = require('debug')('test-server:server');
var http = require('http');
// app 
// debug모듈 콘솔에 로그를 남기는 모듈
// http

/**
 * Get port from environment and store in Express.
 */

var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);
// app.set('port', port)로 서버가 실행될 포트를 설정
// process.env 객체에 PORT 속성이 있다면 그 값을 사용하고, 없다면 기본값으로 3000번 포트를 이용하도록 설정
// app.set(키, 값)을 사용해서 데이터를 저장가능 ***
// 나중에 데이터를 app.get(키)로 가져올 수 있음 ***

/**
 * Create HTTP server.
 */

var server = http.createServer(app);
// http.createServer에 불러온 app 모듈을 넣어줌
// app 모듈이 createServer 메서드의 콜백 함수 역할

/**
 * Listen on provided port, on all network interfaces.
 */

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);
// listen을 하는 부분은 http 웹 서버와 동일
// 서버를 구동했던 것과 동일하게 포트를 연결하고 서버를 실행
// 익스프레스는 그저 콜백 함수 부분을 조금 다르게 만든 것

/**
 * Normalize a port into a number, string, or false.
 */

function normalizePort(val) {
  var port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port >= 0) {
    // port number
    return port;
  }

  return false;
}

/**
 * Event listener for HTTP server "error" event.
 */

function onError(error) {
  if (error.syscall !== 'listen') {
    throw error;
  }

  var bind = typeof port === 'string'
    ? 'Pipe ' + port
    : 'Port ' + port;

  // handle specific listen errors with friendly messages
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use');
      process.exit(1);
      break;
    default:
      throw error;
  }
}

/**
 * Event listener for HTTP server "listening" event.
 */

function onListening() {
  var addr = server.address();
  var bind = typeof addr === 'string'
    ? 'pipe ' + addr
    : 'port ' + addr.port;
  debug('Listening on ' + bind);
}

```



* ***app.js***

```js
var createError = require('http-errors');
var express = require('express');
var path = require('path');
var cookieParser = require('cookie-parser');
var logger = require('morgan');

var indexRouter = require('./routes/index');
var usersRouter = require('./routes/users');

var app = express();
// ecpress를 패키지를 호출하여 app 변수 객체를 만듦
// 이 변수에 각종 기능을 연결

// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'jade');
// app.set 메서드로 익스프레스 앱을 설정 가능

/*
app.use(function(req, res, next) {
    console.log(req.url, '저도 미들웨어입니다.');
    // 이렇게 서버가 받은 요청은 미들웨어를 타고 라우터까지 전달
    next();
    // 반드시 미들웨어 안에서 next();를 호출해야 다음 미들웨어로 넘어감
    // next();는 미들웨어의 흠름을 제어하는 핵심적인 함수
})
*/

/*
app.use(function(req, res, next) {
    console.log('첫 번째 미들웨어');
    next();
}, function(req, res, next) {
    console.log('두 번째 미들웨어');
    next();
}, function(req, res, next) {
    console.log('세 번째 미들웨어');
    next();
})
*/

/*
app.use(logger('dev'), express.json(), express.urlencoded({ extended: false }), cookieParser(), express.static(path.join(__dirname, 'public')));
*/

// morgan (요청에 대한 정보를 콘솔에 기록)
app.use(logger('dev')); // GET / 200 51.267 ms - 1539  // HTTP요청(GET) 주소(/) HTTP상태코드(200) 응답속도(51.267ms) 응답바이트(1539)  // 보통 개발 시 short, dev / 배포 시에는 common, combined
// static (정적인 파일들을 제공 - 익스프레스에 내장되어 require 할 필요가 없음)
app.use(express.static(path.join(__dirname, 'public'))); // 중요
// body-parser (요청의 본문을 해석해주는 미들웨어 - 보통 폼 데이터나 AJAX 요청의 데이터를 처리)
app.use(express.json()); // 익스프레스에 내장되어 require 할 필요가 없음
app.use(express.urlencoded({ extended: false }));
// cookie-parser (요청에 동봉된 쿠키를 해석)
app.use(cookieParser());


app.use('/', indexRouter);
app.use('/users', usersRouter);

// catch 404 and forward to error handler
app.use(function(req, res, next) {
  next(createError(404));
});

// error handler => 에러 핸들러는 변수가 4개임!
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render('error');
});
// app.use로 시작하는 코드는 미들웨어를 연결하는 부분

module.exports = app;
// app 객체를 모듈로 만듦
// bin/www에서 사용된 app 모듈

```





## 2. 미들웨어



미들웨어는 익스프레스의 핵심

요청과 응답의 중간(middle, 미들)에 위치하여 미들웨어

ex) 라우터와 에러 핸들러 또한 미들웨어의 일종

***=> 미들웨어가 익스프레스의 전부***

미들웨어는 요청과 응답을 조작하여 기능을 추가하거나 나쁜 요청을 걸러내기도 함



***미들웨어는 주로 `app.use`와 함께 사용***



`app.use`메서드의 인자로 들어 있는 함수가 미들웨어

<u>(미들웨어는 use 메서드로 app에 장착)</u>



***재일 위에 `app.use(logger('dev'))`부터 시작하여 미들웨어들을 순차적으로 거친 후 라우터에서 클라이언트로 응답을 보냄***

***=> 미들웨어의 순서가 중요***



* `next()` => 다음 미들웨어로

* `next('route')` => 다음 라우터로

* `next(error)` => 에러 핸들러로





### 미들웨어의 종류



#### (1) morgan

***요청에 대한 정보를 콘솔에 기록***

```js
// app.js

...
var logger = require('morgan');
...
app.use(logger('dev'));
...

```

**GET / 200 51.267 ms - 1539** 

HTTP요청(**GET**) 주소(**/**) HTTP상태코드(**200**) 응답속도(**51.267ms**) 응답바이트(**1539**)

개발 시 : **short / dev**

배포 시 : **common / combined**





#### (2) body-parser *(익스프레스에 내장되어 있어 설치할 필요 없음)*

***요청의 본문을 해석해주는 미들웨어 - 보통 폼 데이터나 AJAX 요청의 데이터를 처리***

```js
// app.js

...
var bodyParser = require('body-parser');
...
app.use(bodyParser.json());
app.use(bodyParser.urlenclosed({ extended: false}));
...

```

Raw는 본문이 버퍼 데이터일 때

Text는 본문이 텍스트 데이터일 때 

해석하는 미들웨어

서비스에 적용하고 싶을 경우 body-parser를 설치한 후 추가

`app.use(bodyParser.raw());`

`app.use(bodyParser.text());`





#### (3) cookie-parser

***요청에 동봉된 쿠키를 해석***

```js
// app.js

...
var cookieParser = require('cookie-parser');
...
app.use(cookieParser());
...

```

해석된 쿠키들은 req.cookies **객체**에 들어감

예를 들어 name=zerocho 쿠키를 보냈다면 req.cookies는 `{name: 'zerocho'}`가 됨



`app.use(cookieParser('secret code'));`

이와 같이 첫 번째 인자로 문자열을 넣어 줄수 있음





#### (4) static *(익스프레스에 내장되어 있어 설치할 필요 없음)*

***정적인 파일들을 제공 - `app.use(logger('dev'));`의 바로 아래로 이동***

```js
// app.js

app.use(express.static(path.join(__dirname, 'public')));
```

함수의 인자로 정적 파일들이 담겨 있는 폴더를 지정 => public

public/stylesheets/style.css는 http://localhost:3000/stylesheets/style.css 로 접근 가능

**실제 서버의 폴더 경로에는 public이 들어있지만, 요청 주소에는 public이 들어 있지 않다는 점을 주목**

정적 파일들을 알아서 제공해주므로 fs.readFile로 파일을 직접 읽어 전송할 필요가 없음



`app.use('/img', express.static(path.join(__dirname, 'public')));`

이와 같이 정적 파일을 제공할 주소를 지정할 수 있음

public 폴더 안에 abc.png가 있다면 앞에 /img 경로를 붙인 http://localhost:3000/img/abc.png 주소로 접근 가능





#### (5) express-session *(설치해야됨)*

***세션 관리용 미들웨어 (로그인 등의 이유로 세션을 구현할 때 매우 유용)***

설치: `$ npm i express-session`





#### (6) connect-flash *(설치해야됨)*

***일회성 메시지들을 웹 브라우저에 나타낼 때 좋음***

설치: `$ npm i connect-flash`

