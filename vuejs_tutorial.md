# Vue.js Tutorial



### Data & Method

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Data & Method</h1>
    <h2>{{ greet('night') }}</h2>
    <p>Name : {{ name }}</p>
    <p>Job : {{ job }}</p>
  </div>
  <script src="App.js"></script>
</body>

</html>
```

`<div>` 태그의 id를 지정해주면

App.js 에서 key el에 id를 지정해준다.



***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {
    name: 'Shaun',
    job: 'Ninja'
  },
  methods: {
    greet: function (time) { 
      return `Good ${time} ${this.name}`;
    }
  }
});
```





----



### Data Binding

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Data Binding</h1>
    <a v-bind:href="website">The Net Ninja</a>
    <input type="text" v-bind:value="name" />
    <p v-html="websiteTag"></p>
  </div>
  <script src="App.js"></script>
</body>

</html>
```

***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {
    name: 'Shaun',
    job: 'Ninja',
    website: 'http://www.thenetninja.co.uk',
    websiteTag: '<a href="http://www.thenetninja.co.uk">The Net Ninja Website</a>'
  },
  methods: {
    greet: function (time) { 
      return `Good ${time} ${this.name}`;
    }
  }
});
```



* ***`v-bind`***





----



### Event

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Event</h1>
    <!-- <button v-on:click="age++">Add a Year</button>
    <button v-on:click="age--">Subtract a Year</button> -->
    <!-- <button v-on:click="add">Add a Year</button>
    <button v-on:click="subtract">Subtract a Year</button> -->
    <button @click="add(1)">Add a Year</button>
    <button v-on:click="subtract(1)">Subtract a Year</button>
    <button @dblclick="add(10)">Add 10 Years</button>
    <button v-on:dblclick="subtract(10)">Subtract 10 Years</button>
    <p>My age is {{ age }}</p>
    <div id="canvas" v-on:mousemove="updateXY">{{ x }}, {{ y }}</div>
  </div>
  <script src="App.js"></script>
</body>

</html>
```

***App.js***

````js
new Vue({
  el: '#vue-app',
  data: {
    age: 25,
    x: 0,
    y: 0
  },
  methods: {
    add: function (inc) { 
      this.age+=inc;
    },
    subtract: function (dec) { 
      this.age-=dec;
    },
    updateXY: function (event) { 
      // console.log(event);
      this.x = event.offsetX;
      this.y = event.offsetY;
    }
	// add: function () { 
    //   this.age++;
    // },
    // subtract: function () { 
    //   this.age--;
    // }
  }
});
````

***style.css***

```css
#canvas {
  width: 600px;
  padding: 200px 20px;
  text-align: center;
  border: 1px solid #333;
}
```





----



### Event Modifiers (이벤트 수식어)

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Event Modifiers</h1>
      <!-- once / prevent -->
    <button @click.once="add(1)">Add a Year</button>
    <button v-on:click="subtract(1)">Subtract a Year</button>
    <button @dblclick="add(10)">Add 10 Years</button>
    <button v-on:dblclick="subtract(10)">Subtract 10 Years</button>
    <p>My age is {{ age }}</p>
    <div id="canvas" v-on:mousemove="updateXY">{{ x }}, {{ y }}</div>
    <a v-on:click.prevent="click" href="https://www.google.com">Google</a>
  </div>
  <script src="App.js"></script>
</body>

</html>
```

***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {
    age: 25,
    x: 0,
    y: 0
  },
  methods: {
    add: function (inc) { 
      this.age+=inc;
    },
    subtract: function (dec) { 
      this.age-=dec;
    },
    updateXY: function (event) { 
      // console.log(event);
      this.x = event.offsetX;
      this.y = event.offsetY;
    },
    click: function () { 
      alert("You Clicked Me");
    }
  }
});
```



* `.stop`

  ```html
  <!-- 클릭 이벤트 전파가 중단됩니다 -->
  <a v-on:click.stop="doThis"></a>
  ```

* `.prevent`

  ```html
  <!-- 제출 이벤트가 페이지를 다시 로드 하지 않습니다 -->
  <form v-on:submit.prevent="onSubmit"></form>
  
  <!-- 수식어는 체이닝 가능합니다 -->
  <a v-on:click.stop.prevent="doThat"></a>
  
  <!-- 단순히 수식어만 사용할 수 있습니다 -->
  <form v-on:submit.prevent></form>
  ```

* `.capture`

  ```html
  <!-- 이벤트 리스너를 추가할 때 캡처모드를 사용합니다 -->
  <!-- 즉, 내부 엘리먼트를 대상으로 하는 이벤트가 해당 엘리먼트에서 처리되기 전에 여기서 처리합니다. -->
  <div v-on:click.capture="doThis">...</div>
  ```

* `.self`

  ```html
  <!-- event.target이 엘리먼트 자체인 경우에만 트리거를 처리합니다 -->
  <!-- 자식 엘리먼트에서는 안됩니다 -->
  <div v-on:click.self="doThat">...</div>
  ```

* `.once`

  ```html
  `<!-- 클릭 이벤트는 최대 한번만 트리거 됩니다. --><a v-on:click.once="doThis"></a>`
  ```





----



### Keyboard Events (키 수식어)

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Keyboard Events</h1>
    <label>Name:</label>
    <input type="text" v-on:keyup.enter="logName" />
    <!--enter key 입력 시-->
    <label>Age:</label>
    <input type="text" v-on:keyup.alt.enter="logAge" />
    <!--alt + enter key 입력 시-->
  </div>
  <script src="App.js"></script>
</body>

</html>
```

***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {},
  methods: {
    logName: function () { 
      console.log("you entered your name");
    },
    logAge: function () { 
      console.log("you entered your age"); 
    }
  }
});
```



- `.enter`

  ```html
  `<!-- 위와 같습니다 --><input v-on:keyup.enter="submit"><!-- 약어 사용도 가능합니다 --><input @keyup.enter="submit">`
  ```

- `.tab`

- `.delete` (“Delete” 와 “Backspace” 키 모두를 캡처합니다)

- `.esc`

- `.space`

- `.up`

- `.down`

- `.left`

- `.right`



----



### Two Way Data Binding

***index.html***

````html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Two Way Data Binding</h1>
    <label>Name:</label>
    <input type="text" v-model="name" />
    <span>{{ name }}</span>
    <label>Age:</label>
    <input type="text" v-model="age" />
    <span>{{ age }}</span>
  </div>
  <script src="App.js"></script>
</body>

</html>
````

***App.js***

````js
new Vue({
  el: '#vue-app',
  data: {
    name: '',
    age: ''
  },
  methods: {
    logName: function () { 
      console.log("you entered your name");
    },
    logAge: function () { 
      console.log("you entered your age"); 
    }
  }
});

````



* ***`v-model`***





----



### Computed Properties

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Computed Properties</h1>
    <button v-on:click="a++">Add to A</button>
    <button v-on:click="b++">Add to B</button>
    <p>A - {{ a }}</p>
    <p>B - {{ b }}</p>
    <!-- <p>Age + A = {{ addToA() }}</p>
    <p>Age + B = {{ addToB() }}</p> -->
    <p>Age + A = {{ addToA }}</p>
    <p>Age + B = {{ addToB }}</p>
  </div>
  <script src="App.js"></script>
</body>

</html>

```

***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {
    age: 20,
    a: 0,
    b: 0
  },
  methods: {
    // addToA: function () {
    //   console.log('addToA');
    //   return this.a + this.age;
    // },
    // addToB: function () {
    //   console.log('addToB');
    //   return this.b + this.age;
    // }
  },
  computed: {
    addToA: function () {
      console.log('addToA');
      return this.a + this.age;
    },
    addToB: function () {
      console.log('addToB');
      return this.b + this.age;
    }
  }
});
```



* ***methods vs computed***

* methods

   자신이 참고하고 있는 것 / 자신이 참고하지 않는 값이 변경될 때도 재실행

  Ex) `addToA()`

* computed 

  자신이 참고하고 있는 값이 변경될 때만 재실행

  Ex) `addToA`

  



---



### Dynamic CSS

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Dynamic CSS</h1>
    <h2>Example 1</h2>
    <!-- <div v-bind:class="{red:true, blue:true}"></div> -->
    <!-- <div v-on:click="available=!available" v-bind:class="{available: available}">
      <span>Ryu</span>
    </div> -->
    <h2>Example 2</h2>
    <button v-on:click="nearby=!nearby">Toggle nearby</button>
    <button v-on:click="available=!available">Toggle available</button>
    <div v-bind:class="compClasses">
      <span>Ryu</span>
    </div>
  <script src="App.js"></script>
</body>

</html>

```

***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {
    available: true,
    nearby: false
  },
  methods: {

  },
  computed: {
    compClasses: function () {
      // Example 2
      return {
        available: this.available,
        nearby: this.nearby
      }
    }
  }
});

```

***style.css***

```css
span{
  background: red;
  display: inline-block;
  padding: 10px;
  color: #fff;
  margin: 10px 0;
}

.available span{
  background: green;
}

.nearby span:after{
  content: "nearby";
  margin-left: 10px;
}
```



* `v-on:click="nearby=!nearby"`
* `v-on:click="available=!available"`

* ***`v-bind:class`***





----



### Conditionals (v-if & v-show)

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Conditionals</h1>
    <button v-on:click="error=!error">Toggle Error</button>
    <button v-on:click="success=!success">Toggle Success</button>
    <p v-if="error">There has been an error</p>
    <p v-else-if="success">Whooo, success :)</p>
    <!-- v-if="true"일 경우 보여준다 / v-if="false"일 경우 보여주지 않는다 -->
    <p v-show="error">There has been an error</p>
    <p v-show="success">Whooo, success :)</p>
  </div>
  <script src="App.js"></script>
</body>

</html>

```

***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {
    error: false,
    success: false
  },
  methods: {},
  computed: {}
});

```



* ***`v-if`***

  Ex) `v-if="true or false"`

* ***`v-else-if`***

  

* ***`v-show`***



`v-if / v-show`의 차이 => console 창을 확인!!





---



### Looping with v-for

***index.html***

```html
<!DOCTYPE html>

<html>

<head>
  <meta charset="utf-8">
  <title>VueJS Tutorials</title>
  <link href="style.css" rel="stylesheet" />
  <script src="https://unpkg.com/vue"></script>
</head>

<body>
  <div id="vue-app">
    <h1>Looping through lists</h1>
    <!-- <ul>
      <li v-for="character in characters">{{ character }}</li>
      character는 다른 이름을 지정해줄 수 있음
    </ul>
    <ul>
      <li v-for="ninja in ninjas">{{ ninja.name }} - {{ ninja.age }}</li>
    </ul> -->
    <ul>
      <li v-for="(character, index) in characters">{{ index + 1 }} . {{ character }}</li>
    </ul>
    <ul>
      <li v-for="(ninja, index) in ninjas">{{ index }} . {{ ninja.name }} - {{ ninja.age }}</li>
    </ul>
    <div v-for="(ninja, index) in ninjas">
      <h3>{{ index }} . {{ ninja.name }}</h3>
      <p>{{ ninja.age }}</p>
    </div>
    <template v-for="(ninja, index) in ninjas">
      <h3>{{ index }} . {{ ninja.name }}</h3>
      <p>{{ ninja.age }}</p>
    </template>

    <template v-for="ninja in ninjas">
      <div v-for="(val, key) in ninja">
        <p>{{ key }} - {{ val }}</p>
      </div>
    </template>
    <!-- template은 React.Fragment와 유사!! -->

  </div>
  <script src="App.js"></script>
</body>

</html>

```

***App.js***

```js
new Vue({
  el: '#vue-app',
  data: {
    name: 'jack',
    characters: ['Mario', 'Luigi', 'Yoshi', 'Bowser'],
    ninjas:[
      {name: 'Ryu', age: 25},
      {name: 'Yoshi', age: 35},
      {name: 'Ken', age: 55}
    ]
  },
  methods: {},
  computed: {}
});

```



* ***`v-for`***
* `<template />` 는 `React.Fragment` 와 유사!!





----



## Index

* `v-bind`

  * `v-bind:href`
  * `v-bind:class`

* `v-html`

* `v-on` === `@`
  * `v-on:click`
  * `v-on:dblclick`
  * `@click`
  * `@dblclick`
  * `@click.once` => ***일회성***

* `v-model`

* methods / computed

* `v-if`

* `v-else-if`

* `v-show`

* `v-for`

* `<template />` => `React.Fragment` 와 유사!!

  

