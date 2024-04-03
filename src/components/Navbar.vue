<template>
    <nav class="bg-white border-gray-200 dark:bg-gray-900">
      <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
        <a href="#" class="flex items-center text-white uppercase font-bold" @click.prevent="openSidebar"> VueStore </a>
        <div id="navbar-default">
          <a href="#" class="text-white uppercase font-bold" @click.prevent="openSidebar"> Shopping cart  <span v-if="cartLength > 0" >( {{ cartLength }} )</span>  </a>
        </div>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    methods: {
      openSidebar() {
        this.$emit('open-sidebar');
      }
    },
    props: {
      cartLength: {
        type: Number,
        default: 0
      }
    }
  };
  </script>