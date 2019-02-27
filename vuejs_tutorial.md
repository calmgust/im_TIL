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



## Index

* `v-bind`
  * `v-bind:href`
* `v-html`
* `v-on` === `@`
  * `v-on:click`
  * `v-on:dblclick`
  * `@click`
  * `@dblclick`

