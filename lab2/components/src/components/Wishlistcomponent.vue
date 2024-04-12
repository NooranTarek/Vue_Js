<template>
    <div class="d-flex align-items-baseline justify-content-between p-2 m-2 text-danger">
      <h4 class="text-center" v-if="wishlist.items.length === 0">Sorry, Add Books to Wishlist !!!</h4>
      
      <table v-if="wishlist.items.length > 0" class="table table-bordered table-striped">
        <thead>
          <tr>
            <th>Image</th>
            <th>ISBN</th>
            <th>Name</th>
            <th>Author</th>
            <th>Category</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in wishlist.items" :key="item.book.ISBN">
            <td>
              <img :src="item.book.image" :alt="item.book.name" style="max-width: 100px; max-height: 100px;">
            </td>
            <td>{{ item.book.ISBN }}</td>
            <td>{{ item.book.name }}</td>
            <td>{{ item.book.author }}</td>
            <td>{{ item.book.category }}</td>
            <td>
              <button class="btn btn-outline-danger" @click="removeFromWishlist(index)">Remove</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: ['wishlist'],
    methods: {
      removeFromWishlist(index) {
        this.$emit('removeFromWishlist', index);
      }
    }
  };
  </script>
  
  <style scoped>
  </style>
  
