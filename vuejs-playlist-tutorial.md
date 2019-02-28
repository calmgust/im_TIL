# Vuejs-playlist-tutorial





### The Vue CLI

* `npm i -g vue-cli`

* `vue init <template-name> <project-name>`
* ex) `vue init webpack my-project`
* ex) `vue init webpack-simple my-project`





---



### Vue Files & Root Component

***App.vue***

```vue
<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <p>{{ greeting() }}</p>
  </div>
</template>

<script>
export default {
  // data() {
  //   return {
  //     title: "first Vue file"
  //   };
  // },
  data: function() {
    return {
      title: "first Vue file"
    };
  },
  methods: {
    greeting: function() {
      return "Hello World";
    }
  }
};
</script>

<style>
    
</style>
```





----



### Nesting & Importing Components

***App.vue***

```vue
<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <characters></characters>
  </div>
</template>

<script>
import Test from "./Test";

export default {
  components: {
    characters: Test
  },
  // data() {
  //   return {
  //     title: "first Vue file"
  //   };
  // },
  data: function() {
    return {
      title: "Test App"
    };
  }
};
</script>

<style>
</style>

```

***Test.vue***

````vue
<template>
  <ul>
    <li v-for="character in characters" :key="character">{{ character }}</li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      characters: ["Yoshi", "Mario", "Ryu"]
    };
  }
};
</script>

<style>
</style>

````

***main.js***

```js
import Vue from 'vue'
import App from './App.vue'
// import Test from './Test.vue'
// // App.vue의 script에서 대체할 수 있다.
// Vue.component('characters', Test);

new Vue({
  el: '#app',
  render: h => h(App)
})

```



* **`<li v-for="character in characters" :key="character">{{ character }}</li>`**

  => `v-for` 에서 key를 필요로 할 때!!





----



### Component CSS

***App.vue***

```vue
<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <characters></characters>
  </div>
</template>

<script>
import Test from "./Test";

export default {
  components: {
    characters: Test
  },
  // data() {
  //   return {
  //     title: "first Vue file"
  //   };
  // },
  data: function() {
    return {
      title: "Test App"
    };
  }
};
</script>

<style scoped>
h1 {
  color: orange;
}
/*
하위 컴포넌트의 CSS 영향을 우선적으로 받게 되는데 
하위 컴포넌트의 영향을 받지 않기 위해서는 scoped를 넣어줘야 한다
*/
</style>
```

***Test.vue***

```vue
<template>
  <div>
    <h1>List of Characters</h1>
    <ul>
      <li v-for="character in characters" :key="character">{{ character }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      characters: ["Yoshi", "Mario", "Ryu"]
    };
  }
};
</script>

<style>
h1 {
  color: green;
}
</style>
```



* **`<style scoped>`**





----

