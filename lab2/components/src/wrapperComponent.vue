<template>
  <div id="app">
    <!-- Navbar component -->
    <nav class="navbar bg-dark navbar-dark">
      <div class="container">
        <a class="navbar-brand text-white" href="#" @click.prevent="changeView('books')">Books</a>
        <button class="btn btn-warning" @click="changeView('wishlist')">Wishlist ❤️</button>
        <button class="btn btn-primary" @click="changeView('form')">Form</button>
      </div>
    </nav>

    <!-- Show different components based on the current view -->
    <FormComponent v-if="currentView === 'form'" />
    <Wishlistcomponent v-if="currentView === 'wishlist'" :wishlist="wishlist" @removeFromWishlist="removeFromWishlist" />
    <bookscomponent v-if="currentView === 'books'" :books="books" @addToWishlist="addToWishlist" @isInWishlist="isInWishlist" />
  </div>
</template>

<script>
import FormComponent from './components/formcomponent.vue';
import bookscomponent from './components/bookscomponent.vue';
import Wishlistcomponent from './components/Wishlistcomponent.vue'
export default {
  name: 'wrappercomponent',
  components: {
    FormComponent,
    bookscomponent,
    Wishlistcomponent,
  },
  data() {
    return {
      currentView: 'books', 
      books: [],
      wishlist: {
        items: []
      }
    };
  },
  async created() {
    try {
      const response = await fetch('http://localhost:5001/books');
      if (!response.ok) {
        throw new Error('Failed to fetch data');
      }
      this.books = await response.json();
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  },
  methods: {
    addToWishlist(book) {
      this.wishlist.items.push({ book: book });
    },
    removeFromWishlist(index) {
      this.wishlist.items.splice(index, 1);
    },
    changeView(view) {
      this.currentView = view;
    },
    isInWishlist(book) {
      return this.wishlist.items.some(item => item.book.ISBN === book.ISBN);
    }
  }
};
</script>

<style scoped>
/* Add your scoped styles here */
</style>
