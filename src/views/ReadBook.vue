<!--<template>
  <div>
    <h1 class="alert alert-info">Read a Book</h1>
    <br>
    <br>
    <div class="container">
      <div v-if="readBooks.length > 0" class="row">
        <div v-for="book in readBooks" :key="book.name" class="col-sm-4">
          <img alt="logo" :src="book.image" style="width:200px;height:200px">
          <a :href="book.url" :title="book.description">{{book.name}}</a>
        </div>
      </div>
      <div v-else>no books</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ReadBook",
  props: ["books"],
  data() {
    return {
      readBooks: [
        {
          name: "react",
          description: "react for beginner",
          image: require("../assets/react.png"),
          url: "https://reactjs.org/"
        }
      ]
    };
  },
  async mounted() {
    this.books.forEach(book => {
      this.readBooks.push(book);
    });
  }
};
</script>

<style>
</style>-->


<template>
  <div>
    <h1 class="alert alert-info">Read a Book</h1>
    <br>
    <br>

    <h2>enrolled {{enrolled}}</h2>

    <h2>enrolled books {{enrolledBooks}}</h2>

    <ul class="list-group">
      <li
        v-for="name in enrolledBooks"
        :key="name"
        class="list-group-item active"
        style="width:200px;margin:5px auto"
      >{{name | toCaps}}</li>
    </ul>

    <div class="container">
      <div v-if="readBooks.length > 0" class="row">
        <div v-for="book in readBooks" :key="book.name" class="col-sm-4">
          <img alt="logo" :src="book.image" style="width:200px;height:200px">

          <a :href="book.url" :title="book.description">{{book.name | capitalise}}</a>

          <input type="button" v-model="book.status" @click="changeStatus(book.name)">
        </div>
      </div>

      <div v-else>no books</div>
    </div>
  </div>
</template>



<script>
export default {
  name: "ReadBook",

  props: ["books"],

  data() {
    return {
      readBooks: [
        {
          name: "react",

          description: "react for beginner",

          image: require("../assets/react.png"),

          url: "https://reactjs.org/",

          status: "enroll"
        }
      ],

      enrolledBooks: [],

      enrolled: 0
    };
  },

  mounted() {
    this.books.forEach(book => {
      this.readBooks.push(book);
    });
  },

  methods: {
    changeStatus(nam) {
      this.readBooks.forEach(book => {
        if (book.name === nam)
          if (book.status === "enroll") {
            book.status = "cancel";

            this.enrolledBooks.push(nam);
          } else {
            book.status = "enroll";

            this.enrolledBooks.splice(this.enrolledBooks.indexOf(nam), 1);
          }
      });
    }
  },

  watch: {
    enrolledBooks: {
      handler(value) {
        this.enrolled = value.length;
      }
    }
  },

  filters: {
    toCaps(value) {
      if (value) return value.toUpperCase();
    },

    capitalise(value) {
      if (value) return value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
};
</script>
