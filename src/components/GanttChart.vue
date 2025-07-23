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

const yAxisData = computed(() => props.tasks.map(t => t.name))
const chartData = computed(() => {
  // [[start, end, taskIndex, taskName], ...]
  return props.tasks.flatMap((t, i) =>
    t.periods.map(p => [p.start, p.end, i, t.name])
  )
})

const option = computed(() => ({
  title: {
    text: '项目任务进度',
    left: 'center',
  },
  tooltip: {
    formatter: function(params: any) {
      return `${params.value[3]}<br/>开始: ${params.value[0]}<br/>结束: ${params.value[1]}`
    }
  },
  grid: {
    left: 100,
    right: 40,
    top: 60,
    bottom: 40
  },
  xAxis: {
    type: 'time',
    min: props.minDate || '',
    max: props.maxDate || '',
    axisLabel: { formatter: '{yyyy}-{MM}-{dd}' }
  },
  yAxis: {
    type: 'category',
    data: yAxisData.value
  },
  series: [
    {
      type: 'custom',
      renderItem: function(params: any, api: any) {
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
            height: height
          },
          style: api.style()
        }
      },
      itemStyle: {
        color: '#42b983',
        borderRadius: 6
      },
      encode: {
        x: [0, 1],
        y: 2
      },
      data: chartData.value
    }
  ]
}))
</script> 