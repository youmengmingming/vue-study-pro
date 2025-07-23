<template>
  <v-chart :option="option" autoresize style="height: 400px; width: 100%" />
</template>

<script setup lang="ts">
import { computed } from 'vue'
import VChart from 'vue-echarts'
import { use } from 'echarts/core'
import { BarChart, CustomChart } from 'echarts/charts'
import { GridComponent, TooltipComponent, TitleComponent } from 'echarts/components'
import { CanvasRenderer } from 'echarts/renderers'

use([BarChart, CustomChart, GridComponent, TooltipComponent, TitleComponent, CanvasRenderer])

interface Period {
  start: string
  end: string
  color?: string
  label?: string
}
interface Task {
  name: string
  periods: Period[]
}

const props = defineProps<{
  tasks: Task[]
  minDate?: string
  maxDate?: string
}>()

const currentYear = new Date().getFullYear()
function toFullDate(str: string) {
  // MM-dd HH:mm => yyyy-MM-dd HH:mm
  return `${currentYear}-${str}`
}

const yAxisData = computed(() => props.tasks.map((t) => t.name))
const chartData = computed(() => {
  // [[start, end, taskIndex, taskName, color, label], ...]
  return props.tasks.flatMap((t, i) =>
    t.periods.map((p) => {
      const color =
        p.color ||
        (() => {
          const day = Number(p.start.split('-')[1])
          return day % 2 === 0 ? '#3498db' : '#42b983'
        })()
      return [toFullDate(p.start), toFullDate(p.end), i, t.name, color, p.label || '']
    }),
  )
})

const option = computed(() => ({
  title: {
    text: '项目任务进度',
    left: 'center',
  },
  tooltip: {
    formatter: function (params: any) {
      // 只显示MM-dd HH:mm
      const fmt = (s: string) => s.slice(5)
      return `${params.value[3]}<br/>${params.value[5] ? '标签: ' + params.value[5] + '<br/>' : ''}开始: ${fmt(params.value[0])}<br/>结束: ${fmt(params.value[1])}`
    },
  },
  grid: {
    left: 100,
    right: 40,
    top: 60,
    bottom: 40,
  },
  xAxis: {
    type: 'time',
    min: toFullDate(props.minDate || ''),
    max: toFullDate(props.maxDate || ''),
    axisLabel: {
      formatter: function (value: string) {
        // value为时间戳或字符串，转为Date
        const d = new Date(value)
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
      },
    },
  },
  yAxis: {
    type: 'category',
    data: yAxisData.value,
  },
  series: [
    {
      type: 'custom',
      renderItem: function (params: any, api: any) {
        const categoryIndex = api.value(2)
        const start = api.coord([api.value(0), categoryIndex])
        const end = api.coord([api.value(1), categoryIndex])
        const height = api.size([0, 1])[1] * 0.6
        return {
          type: 'rect',
          shape: {
            x: start[0],
            y: start[1] - height / 2,
            width: end[0] - start[0],
            height: height,
          },
          style: api.style({ fill: api.value(4) }),
          textContent: api.value(5)
            ? {
                type: 'text',
                style: {
                  text: api.value(5),
                  x: (start[0] + end[0]) / 2,
                  y: start[1],
                  fill: '#fff',
                  font: 'bold 12px sans-serif',
                  textAlign: 'center',
                  textVerticalAlign: 'middle',
                },
              }
            : undefined,
          textConfig: api.value(5)
            ? {
                position: 'inside',
              }
            : undefined,
        }
      },
      itemStyle: {
        borderRadius: 6,
      },
      encode: {
        x: [0, 1],
        y: 2,
      },
      data: chartData.value,
    },
  ],
}))
</script>
