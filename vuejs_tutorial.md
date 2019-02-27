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

