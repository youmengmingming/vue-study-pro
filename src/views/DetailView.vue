<template>
  <div class="detail-container">
    <BackHomeButton />
    <div class="details">
      <h1 class="page-title">详情页面</h1>
      <div class="content-sections">
        <section class="detail-section">
          <h2>关于我们</h2>
          <p>
            这是一个示例的详情页面，您可以在这里添加更多关于项目或个人的详细信息。这里可以介绍公司背景、团队文化、发展历程等内容。
          </p>
        </section>

        <section class="detail-section">
          <h2>服务内容</h2>
          <div class="service-grid">
            <div class="service-item">
              <h3>服务项目一</h3>
              <p>详细的服务描述信息</p>
            </div>
            <div class="service-item">
              <h3>服务项目二</h3>
              <p>详细的服务描述信息</p>
            </div>
            <div class="service-item">
              <h3>服务项目三</h3>
              <p>详细的服务描述信息</p>
            </div>
          </div>
        </section>

        <section class="detail-section">
          <h2>联系方式</h2>
          <div class="contact-info">
            <div class="contact-item">
              <strong>邮箱：</strong>
              <span>example@email.com</span>
            </div>
            <div class="contact-item">
              <strong>电话：</strong>
              <span>123-456-7890</span>
            </div>
            <div class="contact-item">
              <strong>地址：</strong>
              <span>示例地址，城市，国家</span>
            </div>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import BackHomeButton from '../components/BackHomeButton.vue'
</script>

<style scoped>
.detail-container {
  min-height: 100vh;
  background: #f5f7fa;
  padding: 2rem;
}

.details {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.page-title {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 3rem;
  font-size: 2.5rem;
}

.content-sections {
  display: grid;
  gap: 2rem;
}

.detail-section {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.detail-section h2 {
  color: #2c3e50;
  margin-bottom: 1.5rem;
  border-bottom: 3px solid #42b983;
  padding-bottom: 0.5rem;
  font-size: 1.8rem;
}

.service-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-top: 1rem;
}

.service-item {
  padding: 1.5rem;
  background: #f8f9fa;
  border-radius: 10px;
  transition: transform 0.3s ease;
}

.service-item:hover {
  transform: translateY(-5px);
}

.service-item h3 {
  color: #42b983;
  margin-bottom: 1rem;
}

.contact-info {
  display: grid;
  gap: 1rem;
}

.contact-item {
  display: flex;
  align-items: center;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 8px;
}

.contact-item strong {
  min-width: 80px;
  color: #42b983;
}

@media (max-width: 768px) {
  .detail-container {
    padding: 1rem;
  }

  .details {
    padding: 1rem;
  }

  .page-title {
    font-size: 2rem;
  }
}
</style>
