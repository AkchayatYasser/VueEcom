<template>
    <div v-if="isOpen" class="sidebar overflow-auto">
      <div class="sidebar-content flex flex-col items-center gap-1">
        <h2 class="text-gray-950 uppercase font-bold">Shopping Cart</h2>
        <ul class="flex flex-col gap-4">
            <li v-for="(item, index) in cart" :key="index" class="flex flex-col">
                <div class="bg-slate-800 rounded-lg p-5 flex flex-col justify-center items-center  ">
                    <img class="h-14 w-14 rounded-full" :src="item.image" alt="Neil image">
                    <p class="text-white"> {{ item.title }} - <span class="font-bold text-gray-400"> ${{ item.price }} </span> </p>
                    <div class="flex gap-4 items-center">
                        <p class="text-white mt-4"> Quantity: {{ item.quantity }} </p>
                        <button class="bg-slate-200 rounded px-1 hover:bg-slate-400" @click="increaseQuantity(index)">+</button>
                        <button class="bg-slate-200 rounded px-1 hover:bg-slate-400" @click="decreaseQuantity(index)">-</button>
                    </div>
                    
                    <button class="text-red-500" @click="removeItem(index)">Remove</button>
                </div>
            </li>
        </ul>
        <p>Total: ${{ calculateTotalPrice().toFixed(2) }}</p>
        
            <button @click="closeSidebar" class="text-white bg-gray-800 hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700">Close</button>
        
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cart: {
        type: Array,
        default: () => []
      },
      isOpen: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      closeSidebar() {
        this.$emit('close-sidebar');
      },
      increaseQuantity(index) {
        this.cart[index].quantity++;
      },
      decreaseQuantity(index) {
        if (this.cart[index].quantity > 1) {
          this.cart[index].quantity--;
        }
      },
      removeItem(index) {
        this.cart.splice(index, 1);
      },
      calculateTotalPrice() {
        return this.cart.reduce((total, item) => {
          return total + item.price * item.quantity;
        }, 0);
      }
    }
  };
  </script>
  
  <style scoped>
  .sidebar {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    width: 300px;
    background-color: white;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    z-index: 1000;
  }
  
  .sidebar-content {
    padding: 20px;
  }
  
  
  </style>