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



### Slots

