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



### Component CSS (scoped)

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



### Nesting Components Examples

***App.vue***

```vue
<template>
  <div>
    <app-header></app-header>
    <app-article></app-article>
    <app-footer></app-footer>
  </div>
</template>

<script>
import Header from "./components/Header";
import Footer from "./components/Footer";
import Article from "./components/Article";

export default {
  components: {
    "app-header": Header,
    "app-footer": Footer,
    "app-article": Article
  },
  data() {
    return {};
  }
};
</script>

<style>
</style>
```

***./components/Header.vue***

```vue
<template>
  <header>
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  data() {
    return {
      title: "Vue Characters"
    };
  }
};
</script>

<style scoped>
header {
  background: lightgreen;
  padding: 10px;
}
h1 {
  color: #222;
  text-align: center;
}
</style>

```

***./components/Footer.vue***

```vue
<template>
  <footer>
    <p>{{ copyright }}</p>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      copyright: "Copyright 2019 Vuejs"
    };
  }
};
</script>

<style scoped>
footer {
  background: #222;
  padding: 6px;
}
p {
  color: lightgreen;
  text-align: center;
}
</style>
```

***./components/Article.vue***

````vue
<template>
  <div id="characters">
    <ul>
      <li
        v-for="character in characters"
        :key="character"
        v-on:click="character.show = !character.show"
      >
        <h2>{{ character.name }}</h2>
        <h3 v-show="character.show">{{ character.speciality }}</h3>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      characters: [
        { name: "Ryu", speciality: "Vue Components", show: false },
        { name: "Crystal", speciality: "HTML Wizardry", show: false },
        { name: "Hitoshi", speciality: "Click Events", show: false },
        { name: "Tango", speciality: "Conditionals", show: false },
        { name: "Kami", speciality: "Webpack", show: false },
        { name: "Yoshi", speciality: "Data Diggin", show: false }
      ]
    };
  }
};
</script>

<style scoped>
#ninjas {
  width: 100%;
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 20px;
  box-sizing: border-box;
}
ul {
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  padding: 0;
}
li {
  flex-grow: 1;
  flex-basis: 300px;
  text-align: center;
  padding: 30px;
  border: 1px solid #222;
  margin: 10px;
}
</style>

````





----



### Props

***App.vue***

```vue
<template>
  <div>
    <app-header></app-header>
    <app-article v-bind:characters="characters"></app-article>
    <app-footer></app-footer>
  </div>
</template>

<script>
import Header from "./components/Header";
import Footer from "./components/Footer";
import Article from "./components/Article";

export default {
  components: {
    "app-header": Header,
    "app-footer": Footer,
    "app-article": Article
  },
  data() {
    return {
      characters: [
        { name: "Ryu", speciality: "Vue Components", show: false },
        { name: "Crystal", speciality: "HTML Wizardry", show: false },
        { name: "Hitoshi", speciality: "Click Events", show: false },
        { name: "Tango", speciality: "Conditionals", show: false },
        { name: "Kami", speciality: "Webpack", show: false },
        { name: "Yoshi", speciality: "Data Diggin", show: false }
      ]
    };
  }
};
</script>

<style>
</style>
```

***./components/Article.vue***

```vue
<template>
  <div id="characters">
    <ul>
      <li
        v-for="character in characters"
        :key="character"
        v-on:click="character.show = !character.show"
      >
        <h2>{{ character.name }}</h2>
        <h3 v-show="character.show">{{ character.speciality }}</h3>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  // props: ['characters'],
  props: {
    characters: {
      type: Array,
      required: true
    }
  },
  data() {
    return {};
  }
};
</script>

<style scoped>
#ninjas {
  width: 100%;
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 20px;
  box-sizing: border-box;
}
ul {
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  padding: 0;
}
li {
  flex-grow: 1;
  flex-basis: 300px;
  text-align: center;
  padding: 30px;
  border: 1px solid #222;
  margin: 10px;
}
</style>
```





----



### Primitive vs Reference Types

***App.vue***

```vue
<template>
  <div>
    <app-header v-bind:title="title"></app-header>
    <app-article v-bind:characters="characters"></app-article>
    <app-footer v-bind:title="title"></app-footer>
  </div>
</template>

<script>
import Header from "./components/Header";
import Footer from "./components/Footer";
import Article from "./components/Article";

export default {
  components: {
    "app-header": Header,
    "app-footer": Footer,
    "app-article": Article
  },
  data() {
    return {
      characters: [
        { name: "Ryu", speciality: "Vue Components", show: false },
        { name: "Crystal", speciality: "HTML Wizardry", show: false },
        { name: "Hitoshi", speciality: "Click Events", show: false },
        { name: "Tango", speciality: "Conditionals", show: false },
        { name: "Kami", speciality: "Webpack", show: false },
        { name: "Yoshi", speciality: "Data Diggin", show: false }
      ],
      title: "Vue Character"
    };
  }
};
</script>

<style>
</style>
```

***./components/Article.vue***

```vue
<template>
  <div id="characters">
    <ul>
      <li
        v-for="character in characters"
        :key="character"
        v-on:click="character.show = !character.show"
      >
        <h2>{{ character.name }}</h2>
        <h3 v-show="character.show">{{ character.speciality }}</h3>
      </li>
    </ul>
    <button v-on:click="deleteCharacter">Delete Character</button>
  </div>
</template>

<script>
export default {
  // props: ['characters'],
  props: {
    characters: {
      type: Array,
      required: true
    }
  },
  data() {
    return {};
  },
  methods: {
    deleteCharacter: function () {
      this.characters.pop();
    }
  }
};
</script>

<style scoped>
#ninjas {
  width: 100%;
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 20px;
  box-sizing: border-box;
}
ul {
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  padding: 0;
}
li {
  flex-grow: 1;
  flex-basis: 300px;
  text-align: center;
  padding: 30px;
  border: 1px solid #222;
  margin: 10px;
}
</style>
```

***./components/Header.vue***

```vue
<template>
  <header>
    <h1 v-on:click="changeTitle">{{ title }}</h1>
  </header>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
    }
  },
  data() {
    return {
      // title: "Vue Characters"
      // => props로 받기 때문에 쓸모없음
    };
  },
  methods: {
    changeTitle: function () {
      this.title = "Vue Wizards"
    }
  }
};
</script>

<style scoped>
header {
  background: lightgreen;
  padding: 10px;
}
h1 {
  color: #222;
  text-align: center;
}
</style>
```

***./components/Footer.vue***

```vue
<template>
  <footer>
    <p>{{ copyright }} {{ title }}</p>
  </footer>
</template>

<script>
export default {
  props: {
    title: {
      type: String
    }
  },
  data() {
    return {
      copyright: "Copyright 2019"
    };
  }
};
</script>

<style scoped>
footer {
  background: #222;
  padding: 6px;
}
p {
  color: lightgreen;
  text-align: center;
}
</style>
```





----



### Events (child to parent)

***App.vue***

```vue
<template>
  <div>
    <app-header v-bind:title="title" v-on:changeTitle="updateTitle($event)"></app-header>
    <app-article v-bind:characters="characters"></app-article>
    <app-footer v-bind:title="title"></app-footer>
  </div>
</template>

<script>
import Header from "./components/Header";
import Footer from "./components/Footer";
import Article from "./components/Article";

export default {
  components: {
    "app-header": Header,
    "app-footer": Footer,
    "app-article": Article
  },
  data() {
    return {
      characters: [
        { name: "Ryu", speciality: "Vue Components", show: false },
        { name: "Crystal", speciality: "HTML Wizardry", show: false },
        { name: "Hitoshi", speciality: "Click Events", show: false },
        { name: "Tango", speciality: "Conditionals", show: false },
        { name: "Kami", speciality: "Webpack", show: false },
        { name: "Yoshi", speciality: "Data Diggin", show: false }
      ],
      title: "Vue Character"
    };
  },
  methods: {
    updateTitle: function (updatedTitle) {
      this.title = updatedTitle;
      // updatedTitle => 하위 컴포넌트에서 보내주는 값
    }
  }
};
</script>

<style>
</style>
```

***./components/Header.vue***

```vue
<template>
  <header>
    <h1 v-on:click="changeTitle">{{ title }}</h1>
  </header>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
    }
  },
  data() {
    return {
      // title: "Vue Characters"
      // => props로 받기 때문에 쓸모없음
    };
  },
  methods: {
    changeTitle: function () {
      // this.title = "Vue Wizards"
      this.$emit('changeTitle', 'Vue Wizards');
      // this.$emit(...)을 쓰는 경우 => child to parent
      // 이벤트를 상위로 올려준다? 
    }
  }
};
</script>

<style scoped>
header {
  background: lightgreen;
  padding: 10px;
}
h1 {
  color: #222;
  text-align: center;
}
</style>
```



* `this.$emit('changeTitle', 'Vue Wizards')`





----



### Event Bus *

***./components/Header.vue***

```vue
<template>
  <header>
    <h1 v-on:click="changeTitle">{{ title }}</h1>
  </header>
</template>

<script>
import { bus } from '../main';

export default {
  props: {
    title: {
      type: String,
    }
  },
  data() {
    return {
      // title: "Vue Characters"
      // => props로 받기 때문에 쓸모없음
    };
  },
  methods: {
    changeTitle: function () {
      // this.title = "Vue Wizards"

      // this.$emit('changeTitle', 'Vue Wizards');
      // this.$emit(...)을 쓰는 경우 => child to parent
      // 이벤트를 상위로 올려준다? 

      this.title = 'Vue Wizards'; // 이 코드를 입력 안해줄 경우 Footer만 변한다!!
      bus.$emit('titleChanged', 'Vue Wizards');
    }
  }
};
</script>

<style scoped>
header {
  background: lightgreen;
  padding: 10px;
}
h1 {
  color: #222;
  text-align: center;
}
</style>
```

***./components/Footer.vue***

```vue
<template>
  <footer>
    <p>{{ copyright }} {{ title }}</p>
  </footer>
</template>

<script>
import { bus } from '../main';

export default {
  props: {
    title: {
      type: String
    }
  },
  data() {
    return {
      copyright: "Copyright 2019"
    };
  },
  created() {
    bus.$on('titleChanged', (data) => {
      this.title = data;
      // data => Header에서 emit해주는 'Vue Wizards'
      // Header를 클릭할 경우 Footer도 변한다.
    })
  }
};
</script>

<style scoped>
footer {
  background: #222;
  padding: 6px;
}
p {
  color: lightgreen;
  text-align: center;
}
</style>
```

***main.js***

```js
import Vue from 'vue'
import App from './App.vue'

export const bus = new Vue();

new Vue({
  el: '#app',
  render: h => h(App)
})
```





---



### Lifecycle Hooks ***

***./components/Article.vue***

```vue
<template>
  <div id="characters">
    <ul>
      <li
        v-for="character in characters"
        :key="character"
        v-on:click="character.show = !character.show"
      >
        <h2>{{ character.name }}</h2>
        <h3 v-show="character.show">{{ character.speciality }}</h3>
      </li>
    </ul>
    <button v-on:click="deleteCharacter">Delete Character</button>
  </div>
</template>

<script>
export default {
  // props: ['characters'],
  props: {
    characters: {
      type: Array,
      required: true
    }
  },
  data() {
    return {};
  },
  methods: {
    deleteCharacter: function () {
      this.characters.pop();
    }
  },
  // lifecycle hooks
  beforeCreate() {
    // alert('beforeCreate');
    console.log('beforeCreate');
  },
  created() {
    // alert('created');
    console.log('created');
  },
  beforeMount() {
    // alert('beforeMount');
    console.log('beforeMount');
  },
  mounted() {
    // alert('mounted');
    console.log('mounted');
  },
  beforeUpdate() {
    // alert('beforeUpdate');
    console.log('beforeUpdate');
  },
  updated() {
    // alert('updated');
    console.log('updated');
  }
};
</script>

<style scoped>
#ninjas {
  width: 100%;
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 20px;
  box-sizing: border-box;
}
ul {
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  padding: 0;
}
li {
  flex-grow: 1;
  flex-basis: 300px;
  text-align: center;
  padding: 30px;
  border: 1px solid #222;
  margin: 10px;
}
</style>
```



* `beforeCreate(){}`
* `created(){}`
* `beforeMount(){}`
* `mounted(){}`
* `beforeUpdate(){}`
* `updated(){}`





---



### Slots *

### (file change)

***App.vue***

```vue
<template>
  <div>
    <form-helper>
      <!-- <h2 slot="title">I am the slot title</h2>
      <h2 slot="title">{{ title }}</h2>
      <p slot="text">I am the paragraph text for the slot</p> -->

      <div slot="form-header">
        <h3>This is the title of the form</h3>
        <p>Information about the form</p>
      </div>
      <div slot="form-fields">
        <input type="text" placeholder="name" required />
        <input type="password" placeholder="password" required />
      </div>
      <div slot="form-controls">
        <button v-on:click="handleSubmit">Submit</button>
      </div>
      
    </form-helper>
  </div>
</template>

<script>
import formHelper from './components/formHelper'

export default {
  components: {
    'form-helper': formHelper
  },
  data() {
    return {
      title: 'I am a dynamic slot title'
    };
  },
  methods: {

  }
};
</script>

<style>
</style>
```

***./components/formHelper.vue***

```vue
<template>
  <!-- <div>
    <slot name="title"></slot>
    <h1>I am the form helper</h1>
    <slot name="text"></slot>
  </div> -->

  <div>

    <h1>Please fill out our form...</h1>

    <form>
      <div id="form-header">
        <slot name="form-header"></slot>
      </div>
      <div id="form-fields">
        <slot name="form-fields"></slot>
      </div>
      <div id="form-controls">
        <slot name="form-controls"></slot>
      </div>
      <div id="useful-links">
        <ul>
          <li><a href="#">Link 1</a></li>
          <li><a href="#">Link 2</a></li>
          <li><a href="#">Link 3</a></li>
          <li><a href="#">Link 4</a></li>
        </ul>
      </div>
    </form>

  </div>
</template>

<script>
export default {
  components: {

  },
  data() {
    return {

    };
  },
  methods: {

  }
};
</script>

<style scoped>
/* h1{
  color: red;
} */
h1{
    text-align: center;
}
form{
    width: 100%;
    max-width: 960px;
    margin: 0 auto;
}
#useful-links ul{
    padding: 0;
}
#useful-links li{
    display: inline-block;
    margin-right: 10px;
}
form > div{
    padding: 20px;
    background: #eee;
    margin: 20px 0;
}
#form-header{
    background: #ddd;
    border: 1px solid #bbb;
}
</style>
```



* **`slot`**





---



### Dynamic Components

***App.vue***

```vue
<template>
  <div>
    <!-- <form-one></form-one>
    <form-two></form-two> -->
    <keep-alive>
      <component v-bind:is="component"></component>
      <!-- <keep-alive> 진행 중 상황 유지 -->
    </keep-alive>
    <button v-on:click="component = 'form-one'">Show form one</button>
    <button v-on:click="component = 'form-two'">Show form two</button>
  </div>
</template>

<script>
import formOne from './components/formOne';
import formTwo from './components/formTwo';

export default {
  components: {
    'form-one': formOne,
    'form-two': formTwo
  },
  data() {
    return {
      component: 'form-one'
    };
  },
  methods: {

  }
};
</script>

<style>
</style>
```

***formOne.vue***

```vue
<template>
  <div>
    <form-helper>
      <div slot="form-header">
        <h3>Form One - Contact Us</h3>
        <p>Fill in this form to contact us</p>
      </div>
      <div slot="form-fields">
        <input type="text" placeholder="name" required />
        <label>Your Message:</label>
        <textarea></textarea>
      </div>
      <div slot="form-controls">
        <button v-on:click="handleSubmit">Send</button>
      </div>
    </form-helper>
  </div>
</template>

<script>
// Imports
import formHelper from './formHelper.vue'
export default {
  components: {
    'form-helper': formHelper
  },
  data () {
    return {
    }
  },
  methods: {
    handleSubmit: function(){
      alert('thanks for submitting form one & contacting us');
    }
  }
}
</script>

<style>
body{
  margin: 0;
  font-family: 'Nunito SemiBold';
}
</style>
```

***formTwo.vue***

```vue
<template>
  <div>
    <form-helper>
      <div slot="form-header">
        <h3>Form Two - Log In</h3>
        <p>Enter your details to log-in</p>
      </div>
      <div slot="form-fields">
        <input type="text" placeholder="username" required />
        <input type="password" placeholder="password" required />
      </div>
      <div slot="form-controls">
        <button v-on:click="handleSubmit">Login</button>
      </div>
    </form-helper>
  </div>
</template>

<script>
// Imports
import formHelper from './formHelper.vue'
export default {
  components: {
    'form-helper': formHelper
  },
  data () {
    return {
    }
  },
  methods: {
    handleSubmit: function(){
      alert('thanks for logging in (form two)');
    }
  }
}
</script>

<style>
body{
  margin: 0;
  font-family: 'Nunito SemiBold';
}
</style>
```



* **`<keep-alive>`** => 진행 중 상황 유지





---



### Input Binding (forms)

***App.vue***

```vue
<template>
  <div>
    <add-blog></add-blog>
  </div>
</template>

<script>
import addBlog from "./components/addBlog";

export default {
  components: {
    "add-blog": addBlog
  },
  data() {
    return {};
  },
  methods: {}
};
</script>

<style>
body {
  margin: 0;
  font-family: "Nunito SemiBold";
}
</style>
```

***./components/addBlog.vue***

```vue
<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2>
    <form>
      <label>Blog Title:</label>
      <!-- <input type="text" v-model="title" required> -->
      <!-- <input type="text" v-model="blog.title" required> -->
      <input type="text" v-model.lazy="blog.title" required>
      <label>Blog Content:</label>
      <!-- <textarea v-model="content"></textarea> -->
      <!-- <textarea v-model="blog.content"></textarea> -->
      <textarea v-model.lazy="blog.content"></textarea>
    </form>
    <div id="preview">
      <h3>Preview blog</h3>
      <!-- <p>Blog title: {{ title }}</p> -->
      <p>Blog title: {{ blog.title }}</p>
      <!-- <p>Blog content: {{ content }}</p> -->
      <p>Blog content:</p>
      <p>{{ blog.content }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // title: "",
      // content: ""
      blog: {
        title: "",
        content: ""
      }
    };
  },
  methods: {}
};
</script>

<style>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 500px;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}
</style>
```



* `v-model.lazy`

  => input box에서 벗어날 때 값을 반영한다.





---



### Checkbox Binding

***./components/addBlog.vue***

```vue
<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2>
    <form>
      <label>Blog Title:</label>
      <!-- <input type="text" v-model="title" required> -->
      <!-- <input type="text" v-model="blog.title" required> -->
      <input type="text" v-model.lazy="blog.title" required>
      <label>Blog Content:</label>
      <!-- <textarea v-model="content"></textarea> -->
      <!-- <textarea v-model="blog.content"></textarea> -->
      <textarea v-model.lazy="blog.content"></textarea>
    </form>
    <div id="preview">
      <h3>Preview blog</h3>
      <!-- <p>Blog title: {{ title }}</p> -->
      <p>Blog title: {{ blog.title }}</p>
      <!-- <p>Blog content: {{ content }}</p> -->
      <p>Blog content:</p>
      <p>{{ blog.content }}</p>

      <p>Blog Categories</p>
      <ul>
        <li v-for="category in blog.categories" :key="category">{{ category }}</li>
      </ul>
    </div>

    <div id="checkboxes">
      <label>Knight</label>
      <input type="checkbox" value="knight" v-model="blog.categories">
      <label>Wizard</label>
      <input type="checkbox" value="wizard" v-model="blog.categories">
      <label>Warrior</label>
      <input type="checkbox" value="warrior" v-model="blog.categories">
      <label>Thief</label>
      <input type="checkbox" value="thief" v-model="blog.categories">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // title: "",
      // content: ""
      blog: {
        title: "",
        content: "",
        categories: []
      }
    };
  },
  methods: {}
};
</script>

<style>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 500px;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}
#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}
#checkboxes label {
  display: inline-block;
}
</style>
```





---



### Select Box Binding (forms)









