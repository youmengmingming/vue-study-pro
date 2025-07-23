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
        <GanttChart :tasks="ganttTasks" :min-date="minDate" :max-date="maxDate" />
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
  { name: '需求分析', periods: [{ start: '06-01 10:00', end: '06-01 12:00' }] },
  { name: 'UI设计', periods: [{ start: '06-01 13:00', end: '06-01 15:00' }] },
  { name: '前端开发', periods: [{ start: '06-01 16:00', end: '06-01 18:00' }] },
  { name: '后端开发', periods: [{ start: '06-01 19:00', end: '06-01 21:00' }] },
  { name: '测试验收', periods: [{ start: '06-01 22:00', end: '06-01 24:00' }] },
])

function getNowStr() {
  const now = new Date()
  const pad = (n: number) => (n < 10 ? '0' + n : '' + n)
  return (
    pad(now.getMonth() + 1) +
    '-' +
    pad(now.getDate()) +
    ' ' +
    pad(now.getHours()) +
    ':' +
    pad(now.getMinutes())
  )
}

function addMinutes(dateStr: string, minutes: number) {
  const d = new Date()
  // 解析 MM-dd HH:mm
  const [md, hm] = dateStr.split(' ')
  const [month, day] = md.split('-').map(Number)
  const [hour, minute] = hm.split(':').map(Number)
  d.setMonth(month - 1)
  d.setDate(day)
  d.setHours(hour)
  d.setMinutes(minute + minutes)
  const pad = (n: number) => (n < 10 ? '0' + n : '' + n)
  return (
    pad(d.getMonth() + 1) +
    '-' +
    pad(d.getDate()) +
    ' ' +
    pad(d.getHours()) +
    ':' +
    pad(d.getMinutes())
  )
}

function randomColor() {
  // 生成亮色
  const h = Math.floor(Math.random() * 360)
  return `hsl(${h}, 70%, 60%)`
}

const periodLabels = ['阶段A', '阶段B', '阶段C', '阶段D', '阶段E', '阶段F', '阶段G', '阶段H']
function randomLabel() {
  return periodLabels[Math.floor(Math.random() * periodLabels.length)]
}

function randomPeriodInRangeMin(start: string, end: string) {
  // 解析 MM-dd HH:mm
  const now = new Date()
  const [mdS, hmS] = start.split(' ')
  const [monthS, dayS] = mdS.split('-').map(Number)
  const [hourS, minuteS] = hmS.split(':').map(Number)
  const [mdE, hmE] = end.split(' ')
  const [monthE, dayE] = mdE.split('-').map(Number)
  const [hourE, minuteE] = hmE.split(':').map(Number)
  const startDate = new Date(now.getFullYear(), monthS - 1, dayS, hourS, minuteS)
  const endDate = new Date(now.getFullYear(), monthE - 1, dayE, hourE, minuteE)
  const range = Math.max(1, Math.floor((endDate.getTime() - startDate.getTime()) / (1000 * 60)) - 2)
  const periodStartOffset = Math.floor(Math.random() * range)
  const periodEndOffset = periodStartOffset + Math.floor(Math.random() * 5) + 1
  const periodStart = new Date(startDate)
  periodStart.setMinutes(startDate.getMinutes() + periodStartOffset)
  const periodEnd = new Date(startDate)
  periodEnd.setMinutes(startDate.getMinutes() + Math.min(periodEndOffset, range + 2))
  const pad = (n: number) => (n < 10 ? '0' + n : '' + n)
  return {
    start:
      pad(periodStart.getMonth() + 1) +
      '-' +
      pad(periodStart.getDate()) +
      ' ' +
      pad(periodStart.getHours()) +
      ':' +
      pad(periodStart.getMinutes()),
    end:
      pad(periodEnd.getMonth() + 1) +
      '-' +
      pad(periodEnd.getDate()) +
      ' ' +
      pad(periodEnd.getHours()) +
      ':' +
      pad(periodEnd.getMinutes()),
    color: randomColor(),
    label: randomLabel(),
  }
}

// 初始化为当前时间
const minDate = ref(getNowStr())
const maxDate = ref(addMinutes(minDate.value, 30))

ganttTasks.value = [
  { name: '需求分析', periods: [randomPeriodInRangeMin(minDate.value, maxDate.value)] },
  { name: 'UI设计', periods: [randomPeriodInRangeMin(minDate.value, maxDate.value)] },
  { name: '前端开发', periods: [randomPeriodInRangeMin(minDate.value, maxDate.value)] },
  { name: '后端开发', periods: [randomPeriodInRangeMin(minDate.value, maxDate.value)] },
  { name: '测试验收', periods: [randomPeriodInRangeMin(minDate.value, maxDate.value)] },
]

function updateTasksAndAxis() {
  // 时间轴右边界+1分钟
  maxDate.value = addMinutes(maxDate.value, 1)
  // 为每个任务追加一段新区间
  ganttTasks.value = ganttTasks.value.map((task) => ({
    ...task,
    periods: [...task.periods, randomPeriodInRangeMin(minDate.value, maxDate.value)],
  }))
}

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
      end: end.toISOString().slice(0, 10),
    })
  }
  return periods
}

function updateTasks() {
  ganttTasks.value = ganttTasks.value.map((task) => ({
    ...task,
    periods: randomPeriods(),
  }))
}

onMounted(() => {
  timer = setInterval(updateTasksAndAxis, 2000)
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
