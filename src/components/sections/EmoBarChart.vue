<script>
import { use } from 'echarts/core';
import { CanvasRenderer } from 'echarts/renderers';
import { BarChart } from 'echarts/charts';
import {
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  GridComponent
} from 'echarts/components';
import VChart from 'vue-echarts';
import { provide } from 'vue';

// 注册所需组件
use([CanvasRenderer, BarChart, TitleComponent, TooltipComponent, LegendComponent, GridComponent]);

export default {
  components: { VChart },
  setup() { provide('THEME_KEY', 'light'); },
  data() {
    // 严格提取原图配色的莫兰迪色系
    const colorWriter = ['#E47E68', '#BA8C64', '#3FB2A4', '#66B272', '#A66CA6', '#DEBB60', '#6980AB'];
    const colorReader = ['#F4C1B6', '#E2C8B1', '#9DDCD3', '#B3DDB8', '#D3B6D3', '#EFDCA1', '#B4C1D6'];

    return {
      // 用于控制自定义图例的交互状态
      showWriter: true,
      showReader: true,
      
      colorWriter: colorWriter,
      colorReader: colorReader,
      emotions: ['Disgust', 'Fear', 'Anger', 'Sadness', 'Neutral', 'Surprise', 'Joy'],
      
      // 数据源
      sources: [
        'ABC News', 'BBC News', 'Independent News', "Today's Headlines", 
        'WeChat Article', 'Weibo Trending', 'The Paper', 'BenignExistence', 
        'RAK', 'FMylife', 'IUTB', 'SocialChemistry', 'Reddit'
      ],
      
      // Writer 数据
      dataW: [
        [12, 21, 8, 49, 5, 133, 54, 9, 6, 110, 2, 14, 45], // Disgust
        [32, 76, 6, 29, 1, 36, 33, 15, 11, 47, 5, 9, 122], // Fear
        [15, 34, 4, 18, 5, 53, 30, 4, 10, 81, 1, 88, 61],  // Anger
        [27, 43, 5, 56, 8, 137, 67, 14, 11, 82, 4, 53, 98],  // Sadness
        [41, 58, 11, 142, 7, 101, 79, 44, 13, 85, 4, 198, 51], // Neutral
        [0, 8, 0, 7, 6, 7, 3, 28, 7, 47, 8, 24, 50],       // Surprise
        [3, 8, 2, 13, 5, 11, 9, 26, 8, 55, 2, 30, 13]      // Joy
      ],

      // Reader 数据
      dataR: [
        [2, 9, 2, 9, 2, 36, 18, 1, 0, 28, 0, 75, 43],      // Disgust
        [31, 60, 4, 37, 1, 29, 19, 1, 0, 23, 1, 0, 13],    // Fear
        [6, 4, 2, 17, 3, 105, 81, 0, 1, 110, 0, 140, 57],  // Anger
        [19, 31, 6, 42, 5, 99, 41, 5, 3, 140, 1, 170, 157],  // Sadness
        [52, 107, 13, 101, 9, 77, 61, 9, 1, 41, 6, 29, 90],  // Neutral
        [14, 24, 6, 75, 15, 107, 44, 5, 1, 117, 0, 1, 62],   // Surprise
        [6, 13, 3, 33, 2, 25, 9, 119, 60, 48, 18, 1, 18]     // Joy
      ]
    };
  },
  computed: {
    // 使用 computed 属性，当 showWriter/showReader 改变时，自动触发图表更新
    chartOption() {
      const grids = [];
      const xAxes = [];
      const yAxes = [];
      const series = [];
      const titles = [];

      // 主标题
      titles.push({
        text: 'Emotion Distribution (Writer vs Reader)',
        left: 'center',
        top: '1%',
        textStyle: { fontSize: 18, color: '#333', fontWeight: 'bold' }
      });

      // 动态生成 7 个切片网格 (Facet Grid)
      this.emotions.forEach((emotion, index) => {
        const leftMargin = 13; // 左侧留出空间给 Y 轴文字
        const gridWidth = 11.2; 
        const gap = 1;
        const currentLeft = leftMargin + index * (gridWidth + gap);

        grids.push({
          left: `${currentLeft}%`,
          width: `${gridWidth}%`,
          top: '12%',
          bottom: '8%'
        });

        titles.push({
          text: emotion,
          left: `${currentLeft + gridWidth / 2}%`,
          top: '7%',
          textAlign: 'center',
          textStyle: { fontSize: 15, fontWeight: 'bold', color: '#444' }
        });

        xAxes.push({
          gridIndex: index,
          type: 'value',
          splitNumber: 2,
          axisLabel: { color: '#888', fontSize: 10 },
          splitLine: { lineStyle: { color: '#f3f3f3' } }
        });

        yAxes.push({
          gridIndex: index,
          type: 'category',
          data: this.sources,
          inverse: true, // 确保源头从上到下显示
          axisLabel: {
            show: index === 0, // 仅在第一个网格(Disgust)显示标签
            color: '#333',
            fontWeight: 'bold',
            fontSize: 12,
            padding: [0, 5, 0, 0]
          },
          axisLine: { show: index === 0, lineStyle: { color: '#ccc' } },
          axisTick: { show: false }
        });

        series.push({
          name: 'Writer',
          type: 'bar',
          xAxisIndex: index,
          yAxisIndex: index,
          data: this.dataW[index],
          itemStyle: { color: this.colorWriter[index], borderRadius: [0, 3, 3, 0] },
          label: { show: true, position: 'right', color: '#555', fontSize: 9, formatter: '{c}' },
          barGap: '0%',
          barCategoryGap: '35%'
        });

        series.push({
          name: 'Reader',
          type: 'bar',
          xAxisIndex: index,
          yAxisIndex: index,
          data: this.dataR[index],
          itemStyle: { color: this.colorReader[index], borderRadius: [0, 3, 3, 0] },
          label: { show: true, position: 'right', color: '#555', fontSize: 9, formatter: '{c}' }
        });
      });

      return {
        title: titles,
        grid: grids,
        xAxis: xAxes,
        yAxis: yAxes,
        series: series,
        
        // 巧妙利用 ECharts 隐藏的 legend 来控制 series 的显隐动画
        legend: {
          show: false, 
          selected: {
            'Writer': this.showWriter,
            'Reader': this.showReader
          }
        },

        tooltip: {
          trigger: 'item',
          backgroundColor: 'rgba(255, 255, 255, 0.95)',
          textStyle: { color: '#333' },
          formatter: (params) => {
            const emotionName = this.emotions[params.seriesIndex / 2 | 0];
            return `<b>${params.name}</b><br/>${emotionName} (${params.seriesName}): ${params.value}`;
          }
        }
      };
    }
  }
};
</script>

<template>
  <div>
    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="22" class="chart-card">
        
        <div class="chart-container">
          
          <div class="custom-legend">
            <div class="legend-item" @click="showWriter = !showWriter" :class="{ inactive: !showWriter }">
              <div class="color-bar">
                <div v-for="(c, i) in colorWriter" :key="'w'+i" :style="{ backgroundColor: c }" class="color-segment"></div>
              </div>
              <span class="legend-text">Writer</span>
            </div>
            
            <div class="legend-item" @click="showReader = !showReader" :class="{ inactive: !showReader }">
              <div class="color-bar">
                <div v-for="(c, i) in colorReader" :key="'r'+i" :style="{ backgroundColor: c }" class="color-segment"></div>
              </div>
              <span class="legend-text">Reader</span>
            </div>
          </div>

          <div class="scroll-wrapper">
            <v-chart class="chart combined-facet-chart" :option="chartOption" autoresize />
          </div>

        </div>

      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
/* 容器相对定位，以便自定义图例绝对定位于左上角 */
.chart-container {
  position: relative;
  width: 100%;
}

/* --- 自定义连续7色图例核心样式 --- */
.custom-legend {
  position: absolute;
  top: 0px;
  left: 10px;
  z-index: 10;
  display: flex;
  flex-direction: column;
  gap: 8px;
  background: rgba(255, 255, 255, 0.8);
  padding: 5px;
  border-radius: 4px;
}
.legend-item {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  transition: opacity 0.3s ease;
}
.legend-item.inactive {
  opacity: 0.3; /* 点击隐藏后变灰 */
}
.color-bar {
  display: flex;
  width: 120px;   /* 色条总长度 */
  height: 12px;   /* 色条高度 */
  border-radius: 2px;
  overflow: hidden;
}
.color-segment {
  flex: 1; /* 平分7段 */
  height: 100%;
}
.legend-text {
  font-size: 13px;
  font-weight: bold;
  color: #333;
  font-family: "Times New Roman", Times, serif; /* 贴合学术感 */
}
/* ---------------------------------- */

.scroll-wrapper {
  width: 100%;
  overflow-x: auto;
}
.chart { 
  min-width: 1000px; /* 防止小屏幕上横向压缩变形 */
  width: 100%; 
}
.combined-facet-chart { 
  height: 850px; 
  margin-top: 10px; 
  margin-bottom: 20px; 
}
.chart-card {
  background: #fff; 
  border-radius: 8px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.05);
  padding: 15px; 
  transition: all 0.3s ease;
  margin-bottom: 40px;
}
.chart-card:hover { 
  box-shadow: 0 4px 20px 0 rgba(0, 0, 0, 0.08); 
}
</style>