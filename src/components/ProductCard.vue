<template>
    <div class="mx-auto w-80 transform overflow-hidden rounded-lg bg-white dark:bg-slate-800 shadow-md duration-300 hover:scale-105 hover:shadow-lg">
      <img :src="product.image" :alt="product.title" class="h-48 w-full object-cover object-center">
      <div class="p-4">
        <h3 @click="showDetails" class="mb-2 text-lg font-medium cursor-pointer dark:text-white text-white">{{ product.title }}</h3>
        <p class="mr-2 text-lg font-semibold text-white">$ {{ product.price }}</p>
        <button @click="addToCart" class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2">Add to Cart</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      product: {
        type: Object,
        required: true
      }
    },
    methods: {
      showDetails() {
    this.$emit('show-details', this.product);
    },
    addToCart() {
    this.$emit('add-to-cart', this.product);
    }
  }
  };
  </script>
  