## Template literals



* **key : back-tick (`)**



```javascript
var str1 = 'code';
var str2 = 'states';

'Welcome to ' + str1 + str2 + '!' // => 'Welcome to codestates!'


// Template literals
`Welcome to ${str1}${str2}!` // => 'Welcome to codestates!'
```



* ***줄 바꿈이 되기 때문에 편하다***

  => 많이 사용해 보자

  ```javascript
  // ES5
  var template = function(username) {
      return `<div>
  	${username}
  </div>`
  }
  
  //-----
  // ES6
  
  var template = (username) => {
      return `<div>
  	${username}
  </div>`
  }
  
  var template = (username) => `<div>
  	${username}
  </div>`
  
  template('Ronaldo');
  
  /*
  <div>
  	Ronaldo
  </div>
  */
  ```




