<template>
  <div class="personal-container">
    <BackHomeButton />
    <div class="profile-header">
      <div class="profile-avatar">
        <img src="https://via.placeholder.com/150" alt="Profile" class="avatar" />
      </div>
      <h1>个人主页</h1>
      <p class="profile-bio">欢迎来到我的个人主页</p>
    </div>

    <div class="profile-content">
      <div class="profile-section">
        <h2>基本信息</h2>
        <div class="info-grid">
          <div class="info-item">
            <span class="label">姓名</span>
            <span class="value">张三</span>
          </div>
          <div class="info-item">
            <span class="label">职业</span>
            <span class="value">软件工程师</span>
          </div>
          <div class="info-item">
            <span class="label">位置</span>
            <span class="value">北京</span>
          </div>
          <div class="info-item">
            <span class="label">邮箱</span>
            <span class="value">example@email.com</span>
          </div>
        </div>
      </div>

      <div class="profile-section">
        <h2>技能专长</h2>
        <div class="skills-grid">
          <div class="skill-item">
            <h3>前端开发</h3>
            <div class="skill-bar" style="width: 90%"></div>
          </div>
          <div class="skill-item">
            <h3>后端开发</h3>
            <div class="skill-bar" style="width: 85%"></div>
          </div>
          <div class="skill-item">
            <h3>UI设计</h3>
            <div class="skill-bar" style="width: 75%"></div>
          </div>
        </div>
      </div>

      <div class="profile-section">
        <h2>统计数据</h2>
        <div class="stats-grid">
          <div class="stat-card">
            <span class="stat-number">12</span>
            <span class="stat-label">项目</span>
          </div>
          <div class="stat-card">
            <span class="stat-number">256</span>
            <span class="stat-label">关注者</span>
          </div>
          <div class="stat-card">
            <span class="stat-number">128</span>
            <span class="stat-label">获赞</span>
          </div>
        </div>
      </div>
      <!-- 新增甘特图卡片 -->
      <a-card title="任务甘特图" style="margin-top: 2rem">
        <GanttChart :tasks="ganttTasks" min-date="2024-06-01" max-date="2024-06-30" />
      </a-card>
    </div>
  </div>
</template>

<script setup lang="ts">
import BackHomeButton from '../components/BackHomeButton.vue'
import { ref, onMounted, onUnmounted } from 'vue'
import { Card as ACard } from 'ant-design-vue'
import 'ant-design-vue/dist/reset.css'
import GanttChart from '../components/GanttChart.vue'

const ganttTasks = ref([
  { name: '需求分析', periods: [ { start: '2024-06-01', end: '2024-06-04' } ] },
  { name: 'UI设计', periods: [ { start: '2024-06-03', end: '2024-06-08' } ] },
  { name: '前端开发', periods: [ { start: '2024-06-07', end: '2024-06-18' } ] },
  { name: '后端开发', periods: [ { start: '2024-06-10', end: '2024-06-22' } ] },
  { name: '测试验收', periods: [ { start: '2024-06-20', end: '2024-06-28' } ] }
])

let timer: any = null

function randomPeriods() {
  const base = new Date('2024-06-01')
  const maxDay = 29
  const periods = []
  const count = Math.floor(Math.random() * 3) + 1 // 1~3段
  for (let i = 0; i < count; i++) {
    const startOffset = Math.floor(Math.random() * (maxDay - 1))
    const endOffset = startOffset + Math.floor(Math.random() * 7) + 1
    const start = new Date(base)
    start.setDate(base.getDate() + startOffset)
    const end = new Date(base)
    end.setDate(base.getDate() + Math.min(endOffset, maxDay))
    periods.push({
      start: start.toISOString().slice(0, 10),
      end: end.toISOString().slice(0, 10)
    })
  }
  return periods
}

function updateTasks() {
  ganttTasks.value = ganttTasks.value.map(task => ({
    ...task,
    periods: randomPeriods()
  }))
}

onMounted(() => {
  timer = setInterval(updateTasks, 2000)
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
</script>

<style scoped>
.personal-container {
  min-height: 100vh;
  background: #f5f7fa;
  padding: 2rem;
}

.profile-header {
  text-align: center;
  margin-bottom: 3rem;
}

.profile-avatar {
  margin-bottom: 1rem;
}

.avatar {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: 4px solid white;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.profile-bio {
  color: #666;
  max-width: 600px;
  margin: 1rem auto;
}

.profile-content {
  max-width: 1200px;
  margin: 0 auto;
}

.profile-section {
  background: white;
  border-radius: 15px;
  padding: 2rem;
  margin-bottom: 2rem;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.profile-section h2 {
  color: #2c3e50;
  margin-bottom: 2rem;
  border-bottom: 3px solid #42b983;
  padding-bottom: 0.5rem;
}

.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
}

.info-item {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.label {
  color: #666;
  font-size: 0.9rem;
}

.value {
  font-size: 1.1rem;
  color: #2c3e50;
}

.skills-grid {
  display: grid;
  gap: 1.5rem;
}

.skill-item h3 {
  margin-bottom: 0.5rem;
  color: #2c3e50;
}

.skill-bar {
  height: 8px;
  background: #42b983;
  border-radius: 4px;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 2rem;
}

.stat-card {
  text-align: center;
  padding: 1.5rem;
  background: #f8f9fa;
  border-radius: 10px;
  transition: transform 0.3s ease;
}

.stat-card:hover {
  transform: translateY(-5px);
}

.stat-number {
  display: block;
  font-size: 2rem;
  font-weight: bold;
  color: #42b983;
}

.stat-label {
  color: #666;
  margin-top: 0.5rem;
  display: block;
}

@media (max-width: 768px) {
  .personal-container {
    padding: 1rem;
  }

  .profile-section {
    padding: 1.5rem;
  }

  .info-grid {
    grid-template-columns: 1fr;
  }
}
</style>
