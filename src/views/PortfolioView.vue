<template>
  <div class="portfolio-container">
    <BackHomeButton />
    <h1 class="page-title">作品展示</h1>
    <div class="portfolio-grid">
      <div v-for="(item, index) in portfolioItems" :key="index" class="portfolio-item">
        <img :src="item.image" :alt="item.title" />
        <div class="portfolio-info">
          <h3>{{ item.title }}</h3>
          <p>{{ item.description }}</p>
          <div class="portfolio-tags">
            <span class="tag">Vue.js</span>
            <span class="tag">TypeScript</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import BackHomeButton from '../components/BackHomeButton.vue'

const portfolioItems = [
  {
    title: '项目一',
    description: '这是一个示例项目描述，展示了项目的主要功能和特点。',
    image: 'https://via.placeholder.com/600x400',
  },
  {
    title: '项目二',
    description: '另一个精彩的项目展示，包含了创新的设计理念。',
    image: 'https://via.placeholder.com/600x400',
  },
  {
    title: '项目三',
    description: '创意设计作品展示，突出了独特的视觉效果。',
    image: 'https://via.placeholder.com/600x400',
  },
  {
    title: '项目四',
    description: '最新完成的开源项目，获得了广泛好评。',
    image: 'https://via.placeholder.com/600x400',
  },
]
</script>

<style scoped>
.portfolio-container {
  min-height: 100vh;
  background: #f5f7fa;
  padding: 2rem;
}

.page-title {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 3rem;
  font-size: 2.5rem;
}

.portfolio-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  padding: 0 1rem;
}

.portfolio-item {
  background: white;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.portfolio-item:hover {
  transform: translateY(-10px);
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.15);
}

.portfolio-item img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.portfolio-item:hover img {
  transform: scale(1.05);
}

.portfolio-info {
  padding: 1.5rem;
}

.portfolio-info h3 {
  font-size: 1.5rem;
  color: #2c3e50;
  margin-bottom: 0.8rem;
}

.portfolio-info p {
  color: #666;
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.portfolio-tags {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.tag {
  background: #e9ecef;
  color: #42b983;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  .portfolio-container {
    padding: 1rem;
  }

  .portfolio-grid {
    grid-template-columns: 1fr;
  }

  .portfolio-item img {
    height: 200px;
  }
}
</style>
