<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="app-container">
    <RouterView />
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  width: 100vw;
  margin: 0;
  padding: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  background-size: cover;
  position: relative;
  overflow: hidden;
}

.auth-buttons {
  position: fixed;
  top: 2rem;
  right: 2rem;
  z-index: 10;
}

.auth-btn {
  padding: 0.8rem 2rem;
  border: none;
  border-radius: 25px;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.login {
  background: #42b983;
  color: white;
}

.logout {
  background: #ff7675;
  color: white;
}

.main-content {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  width: 100vw;
  padding: 0;
}

.main-buttons {
  display: flex;
  gap: 3rem;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 0 2rem;
}

.main-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 280px;
  height: 280px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 30px;
  text-decoration: none;
  color: #2c3e50;
  font-size: 1.8rem;
  font-weight: bold;
  transition: all 0.3s ease;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.main-btn:hover {
  transform: translateY(-15px) scale(1.05);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
  background: white;
}

@media (max-width: 768px) {
  .main-buttons {
    flex-direction: column;
    gap: 2rem;
  }

  .main-btn {
    width: 90vw;
    max-width: 400px;
    height: 120px;
    font-size: 1.5rem;
  }
}
</style>
