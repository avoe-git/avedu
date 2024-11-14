<template>
    <div>
      <h2>Resources for {{ subject }}</h2>
      <button @click="addBook">Add Book</button>
      <div v-for="book in books" :key="book.id">
        <h3 @click="openBook(book)">{{ book.title }}</h3>
      </div>
  
      <BookView v-if="selectedBook" :book="selectedBook" />
    </div>
  </template>
  
  <script>
  import BookView from "./BookView.vue";
  
  export default {
    props: ["subject"],
    data() {
      return {
        books: [],
        selectedBook: null
      };
    },
    methods: {
      addBook() {
        const title = prompt("Enter book title:");
        if (title) this.books.push({ id: Date.now(), title });
      },
      openBook(book) {
        this.selectedBook = book;
      }
    },
    components: {
      BookView
    }
  };
  </script>
  