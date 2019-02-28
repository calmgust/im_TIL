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

