<!--<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  }
}
</script>-->
<template>
  <div id="app">
    <div @click="setFalse()">
      <img alt="Vue logo" src="../assets/logo.png">
      <button @click="getName" class="btn btn-primary" style="margin:20px">click to enter your name</button>
      <span>welcome {{firstName}}</span>
      <br>
      <br>
    </div>

    <div>
      <router-link
        to="/AddBook"
        class="btn btn-primary"
        style="margin:20px"
        @getAddedBook="pushAddedBook"
      >AddBook</router-link>
      <router-link
        :to="{name:'ReadBook', params:{books}}"
        class="btn btn-info"
        style="margin:20px"
      >ReadBook</router-link>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      message: "Welcome to Your Vue.js App",
      firstName: "",
      books: [
        {
          name: "vueJs",
          description: "vuejs for beginner",
          image: require("../assets/logo.png"),
          url: "https://vuejs.org/",
          status: enroll
        },
        {
          name: "angularjs",
          description: "angularjs for beginner",
          image: require("../assets/ang.png"),
          url: "https://angularjs.org/",
          status: enroll
        }
      ]
    };
  },
  methods: {
    getName() {
      this.firstName = prompt("enter your name");
    },
    pushAddedBook(book) {
      this.books.push(book);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

