<template>
  <div>
    <Navbar @open-sidebar="toggleSidebar" :cartLength="cart.length" />
    <Products :cart="cart" @add-to-cart="addToCart" />
    <Sidebar :cart="cart" :is-open="sidebarOpen" @close-sidebar="toggleSidebar" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Navbar from './components/Navbar.vue';
import Products from './components/Products.vue';
import Sidebar from './components/Sidebar.vue';

const cart = ref([]);
const sidebarOpen = ref(false);

function toggleSidebar() {
  sidebarOpen.value = !sidebarOpen.value;
}

function addToCart(product) {
  const existingProductIndex = cart.value.findIndex(item => item.id === product.id);
  if (existingProductIndex !== -1) {
    cart.value[existingProductIndex].quantity++;
  } else {
    product.quantity = 1;
    cart.value.push(product);
  }
}
</script>