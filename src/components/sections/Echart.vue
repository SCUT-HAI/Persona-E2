<script>

import { use } from 'echarts/core';
import { CanvasRenderer } from 'echarts/renderers';
import { PieChart } from 'echarts/charts';
import {
  TitleComponent,
  TooltipComponent,
  LegendComponent,
} from 'echarts/components';
import VChart, { THEME_KEY } from 'vue-echarts';
import { ref, provide } from 'vue';

use([
  CanvasRenderer,
  PieChart,
  TitleComponent,
  TooltipComponent,
  LegendComponent,
]);

export default {
  components: {
    VChart,
  },
  setup() {
    provide('THEME_KEY', 'light');
  },
  data() {
    return {
      option: {
        // 使用echarts设置属性和数据
        title: {
            text: 'Subjective Divergence Subset (SDS) Distribution',
            left: 'center',
        },
        tooltip: {
            trigger: 'item',
            formatter: '{a} <br/>{b} : {c} ({d}%)',
        },
        legend: {
            orient: 'horizontal',
            left: 'center',
            top: 'bottom',
            data: ['News', 'Social Media', 'Life-Experience'],
        },
        series: [
          {
            name: 'SDS Counts',
            type: 'pie',
            radius: '50%',
            center: ['50%', '50%'],
            data: [
              { value: 257, name: 'News' },
              { value: 69, name: 'Social Media' },
              { value: 87, name: 'Life-Experience' },
            ],
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: 'rgba(0, 0, 0, 0.5)',
              },
            },
          },
        ],
      }
    }
  }
}
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Quantitative Results</h1>
    </el-row>

    <!-- echarts 图表 -->
    <el-row justify="center">
      <el-col :xs="24" :sm="20" :md="16" :lg="12" :xl="12">
        <v-chart class="chart" :option="option" autoresize />
      </el-col>
    </el-row>
  </div>
  
</template>

<style scoped>
/* 图表属性 */
.chart {
  height: 300px;
  margin-top: 20px;
}
</style>