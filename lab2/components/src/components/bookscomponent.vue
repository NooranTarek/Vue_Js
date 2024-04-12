<template>
  <div class="row">
    <div class="col-sm-4 mt-4" v-for="book in books" :key="book.ISBN">
      <div class="card mt-4">
        <div class="image">
          <img :src="book.image" :alt="book.name" />
        </div>
        <div class="card-inner">
          <div class="header">
            <h2>{{ book.name }}</h2>
            <h3>{{ book.author }}</h3>
          </div>
          <div class="content">
            <p>Category: {{ book.category }}</p>
            <p :class="{ 'less': book.pages < 50 , 'more': book.pages >= 50 }">Pages: {{ book.pages }}</p>
            <p>Price : {{ formatCurrency(book.price) }}</p> 
            <p>ISBN: {{ book.ISBN }}</p>
            <button :disabled="isInWishlist(book)" @click="addToWishlist(book)" :class="{ 'btn-disabled': isInWishlist(book) }">Add to Wishlist</button>
            <span class="heart-icon">❤️</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['books'],
  methods: {
    addToWishlist(book) {
      this.$emit('addToWishlist', book); 
    },
    isInWishlist(book) {
      this.$emit('isInWishlist', book); 
    },
    formatCurrency(price) {
      return new Intl.NumberFormat('ar-SA', { style: 'currency', currency: 'SAR' }).format(price);
    }
  }
};
</script>

<style scoped>
.card {
  width: 100%;
  height: 100%;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card .image {
  width: 100%;
  height: 200px; /* Specify the desired height */
  overflow: hidden;
}

.card .image img {
  width: 100%;
  height: auto;
  max-width: 100%;
  max-height: 100%;
  object-fit: contain; /* Maintain aspect ratio and fit entire image */
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
}

.card .card-inner {
  padding: 15px;
}

.card .header h2 {
  margin: 0;
}

.card .header h3 {
  margin: 5px 0;
}

.card .content p {
  margin: 5px 0;
}

.card .content button {
  padding: 5px 10px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

.card .content .heart-icon {
  color: red;
  margin-left: 5px;
  font-size: 18px;
}

.less {
  color: red;
}

.more {
  color: green;
}
</style>
