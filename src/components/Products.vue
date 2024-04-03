<template>
    <div class="flex flex-col mt-5 justify-center items-center">
      <input type="text" v-model="searchQuery" placeholder="Search products" class="block w-80 p-4 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 ">
      <div class="grid grid-cols-2 gap-4 mt-7 md:grid-cols-3 lg:grid-cols-4">
        <div v-for="product in filteredProducts" :key="product.id">
            <product-card :product="product" @add-to-cart="addToCart" @show-details="showProductDetails" />
        </div>
      </div>
      <div v-if="selectedProduct" class="product-details-modal w-80">
        <div class="product-details-content">
          <img :src="selectedProduct.image" :alt="selectedProduct.title" class="h-28 w-fit object-cover object-center">
          <h2 class="font-bold">{{ selectedProduct.title }}</h2>
          <p class="w-96">{{ selectedProduct.description }}</p>
          <p class=" font-semibold text-gray-600">Price: ${{ selectedProduct.price }}</p>
          <button @click="closeProductDetails" class="text-white bg-gray-800 hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700">Close</button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
import axios from 'axios';
import ProductCard from './ProductCard.vue';
import { ref, onMounted, computed, getCurrentInstance } from 'vue';

const instance = getCurrentInstance();
const emit = instance.emit;

const products = ref([]);
const searchQuery = ref('');
const selectedProduct = ref(null);

const filteredProducts = computed(() => {
  return products.value.filter(product => {
    return product.title.toLowerCase().includes(searchQuery.value.toLowerCase());
  });
});

onMounted(async () => {
  await fetchProducts();
});

const fetchProducts = async () => {
  try {
    const response = await axios.get('https://fakestoreapi.com/products');
    products.value = response.data;
  } catch (error) {
    console.error('Error fetching products:', error);
  }
};

const addToCart = (product) => {
  console.log('Product added to cart:', product);
  emit('add-to-cart', product);
};

const showProductDetails = (product) => {
  selectedProduct.value = product;
};

const closeProductDetails = () => {
  selectedProduct.value = null;
};
</script>


  
  <style scoped>
  .product-details-modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .product-details-content {
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
  }
  

  </style>
  