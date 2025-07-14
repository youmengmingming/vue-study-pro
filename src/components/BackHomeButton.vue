<template>
  <RouterLink to="/" class="back-home-btn"> 返回主页 </RouterLink>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<style scoped>
.back-home-btn {
  position: fixed;
  top: 2rem;
  right: 2rem;
  padding: 0.8rem 1.5rem;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 25px;
  font-size: 1rem;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.back-home-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
  background: #3aa876;
}
</style>
