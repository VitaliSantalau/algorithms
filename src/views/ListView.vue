<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>


<template>
  <div class="container">
    <RouterLink to="/buble_sort">
      <img src="../assets/images/socks_blue.jpg" />
      <h2>Bubble sort</h2>
      <p>bubble sort algorithm using javascript</p>
    </RouterLink>
    </div>
</template>


<style scoped>
  .container {
    width: 200px;
    height: 300px;
  }
</style>
