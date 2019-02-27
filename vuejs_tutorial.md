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



## Index

* `v-bind`
  * `v-bind:href`
* `v-html`
* `v-on` === `@`
  * `v-on:click`
  * `v-on:dblclick`
  * `@click`
  * `@dblclick`
  * `@click.once` => ***일회성***

