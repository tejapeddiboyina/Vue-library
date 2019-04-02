<template>
  <div>
    <h1 class="alert alert-info">Add a new Book</h1>

    <label>Book Name:</label>
    <input type="text" placeholder="book name" v-model="bookName">
    <p v-if="nameError" class="alert alert-warning">Book name should be atleast 4 letters</p>
    <br>
    <br>
    <label>Description:</label>
    <input type="texfield" placeholder="book description" v-model="description">
    <p v-if="descpError" class="alert alert-warning">Description should be long enough</p>
    <br>
    <br>
    <input type="radio" name="check" @click="free=true" checked>free
    <input type="radio" name="check" @click="isFree()">sell
    <br>
    <br>
    <div v-if="!free">
      <label>Book amount:</label>
      <input type="number" placeholder="enter book amount" v-model="amount">
    </div>
    <br>
    <br>
    <button @click="addBook()" class="btn btn-default" style="margin:20px">add</button>
    <input
      type="button"
      @click="getAddedBooks()"
      class="btn btn-default"
      style="margin:20px"
      value="get added books"
    >

    <div v-if="showBooks">
      <div v-if="books.length > 0">
        <div v-for="book in books" :key="book.name">{{book.name}} | {{book.description}}</div>
      </div>
      <div v-else>no books</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddBook",
  data() {
    return {
      books: [],
      bookName: "",
      description: "",
      free: true,
      showBooks: false,
      nameError: false,
      descpError: false,
      book: {}
    };
  },
  methods: {
    isFree() {
      this.free = false;
    },
    addBook() {
      this.checkError();
      if (this.isError) {
        this.book = {
          name: this.bookName,
          description: this.description,
          free: this.free
        };
        this.books.push(this.book);
        this.reset();
        this.$emit("getAddedBook", this.book);
      }
    },
    checkError() {
      if (this.bookName.length < 3) {
        this.nameError = true;
      } else {
        this.nameError = false;
      }
      if (this.description.length < 10) {
        this.descpError = true;
      } else {
        this.descpError = false;
      }
    },
    getAddedBooks() {
      this.showBooks = true;
    },
    reset() {
      this.bookName = "";
      this.description = "";
      this.free = true;
      this.nameError = false;
      this.descpError = false;
    }
  },
  computed: {
    isError() {
      return this.nameError == false && this.descpError == false ? true : false;
    }
  }
};
</script>
