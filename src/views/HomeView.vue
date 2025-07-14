<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { ref } from 'vue'

const isLoggedIn = ref(false)

const handleLogin = () => {
  isLoggedIn.value = true
}

const handleLogout = () => {
  isLoggedIn.value = false
}

const btnBackgrounds = {
  personal:
    'https://img.freepik.com/free-vector/abstract-business-professional-background-banner-design-multiple-geometric-shapes_1017-14798.jpg',
  portfolio:
    'https://img.freepik.com/free-photo/flat-lay-workstation-with-copy-space-laptop_23-2148430879.jpg',
  detail:
    'https://img.freepik.com/free-vector/gradient-network-connection-background_23-2148865393.jpg',
}
</script>

<template>
  <div class="auth-buttons">
    <button v-if="!isLoggedIn" @click="handleLogin" class="auth-btn login">登录</button>
    <button v-else @click="handleLogout" class="auth-btn logout">退出</button>
  </div>

  <div class="home-container">
    <div class="background-overlay"></div>
    <div class="main-content">
      <div class="main-buttons">
        <RouterLink
          to="/personal"
          class="main-btn"
          :style="{ backgroundImage: `url(${btnBackgrounds.personal})` }"
        >
          <div class="btn-content">个人主页</div>
        </RouterLink>
        <RouterLink
          to="/portfolio"
          class="main-btn"
          :style="{ backgroundImage: `url(${btnBackgrounds.portfolio})` }"
        >
          <div class="btn-content">作品展示</div>
        </RouterLink>
        <RouterLink
          to="/detail"
          class="main-btn"
          :style="{ backgroundImage: `url(${btnBackgrounds.detail})` }"
        >
          <div class="btn-content">详情</div>
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-container {
  min-height: 100vh;
  width: 100vw;
  margin: 0;
  padding: 0;
  position: relative;
  overflow: hidden;
  background-image: url('https://images.pexels.com/photos/147411/italy-mountains-dawn-daybreak-147411.jpeg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

.background-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  z-index: 1;
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
  position: relative;
  z-index: 2;
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
  border-radius: 30px;
  text-decoration: none;
  font-size: 1.8rem;
  font-weight: bold;
  transition: all 0.3s ease;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  position: relative;
  overflow: hidden;
  background-size: cover;
  background-position: center;
}

.main-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  transition: all 0.3s ease;
}

.main-btn:hover::before {
  background: rgba(0, 0, 0, 0.2);
}

.btn-content {
  position: relative;
  z-index: 1;
  color: white;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  padding: 1rem;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 15px;
  backdrop-filter: blur(5px);
  transition: all 0.3s ease;
}

.main-btn:hover {
  transform: translateY(-15px) scale(1.05);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
}

.main-btn:hover .btn-content {
  background: rgba(0, 0, 0, 0.5);
  transform: scale(1.1);
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

  .btn-content {
    padding: 0.5rem 1rem;
  }
}
</style>
