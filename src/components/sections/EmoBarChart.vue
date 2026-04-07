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

// 注册所需组件（柱状图、网格布局、标题、提示框、图例）
use([CanvasRenderer, BarChart, TitleComponent, TooltipComponent, LegendComponent, GridComponent]);

export default {
  components: { VChart },
  setup() { provide('THEME_KEY', 'light'); },
  data() {
    // ================= 1. 数据精确提取与映射 =================
    // Y轴：数据来源 (逆序排列以符合从上到下的阅读习惯，通过 inverse: true 实现)
    const sources = [
      'ABC News', 'BBC News', 'Independent News', "Today's Headlines", 
      'WeChat Article', 'Weibo Trending', 'The Paper', 'BenignExistence', 
      'RAK', 'FMylife', 'IUTB', 'SocialChemistry', 'Reddit'
    ];

    // Writer (作者) 的情绪数值
    const disgustW = [12, 21, 8, 49, 5, 133, 54, 9, 6, 110, 2, 14, 45];
    const fearW = [32, 76, 6, 29, 1, 36, 33, 15, 11, 47, 5, 9, 122];
    const angerW = [15, 34, 4, 18, 5, 53, 30, 4, 10, 81, 1, 88, 61];
    const sadnessW = [27, 43, 5, 56, 8, 137, 67, 14, 11, 82, 4, 53, 98];
    const neutralW = [41, 58, 11, 142, 7, 101, 79, 44, 13, 85, 4, 198, 51];
    const surpriseW = [0, 8, 0, 7, 6, 7, 3, 28, 7, 47, 8, 24, 50];
    const joyW = [3, 8, 2, 13, 5, 11, 9, 26, 8, 55, 2, 30, 13];

    // Reader (读者) 的情绪数值
    const disgustR = [2, 9, 2, 9, 2, 36, 18, 1, 0, 28, 0, 75, 43];
    const fearR = [31, 60, 4, 37, 1, 29, 19, 1, 0, 23, 1, 0, 13];
    const angerR = [6, 4, 2, 17, 3, 105, 81, 0, 1, 110, 0, 140, 57];
    const sadnessR = [19, 31, 6, 42, 5, 99, 41, 5, 3, 140, 1, 170, 157];
    const neutralR = [52, 107, 13, 101, 9, 77, 61, 9, 1, 41, 6, 29, 90];
    const surpriseR = [14, 24, 6, 75, 15, 107, 44, 5, 1, 117, 0, 1, 62];
    const joyR = [6, 13, 3, 33, 2, 25, 9, 119, 60, 48, 18, 1, 18];

    // ================= 2. 颜色与配置项生成 =================
    const emotions = ['Disgust', 'Fear', 'Anger', 'Sadness', 'Neutral', 'Surprise', 'Joy'];
    
    // 严格提取原图配色的莫兰迪色系 (深色代表 Writer，浅色代表 Reader)
    const colorWriter = ['#E47E68', '#BA8C64', '#3FB2A4', '#66B272', '#A66CA6', '#DEBB60', '#6980AB'];
    const colorReader = ['#F4C1B6', '#E2C8B1', '#9DDCD3', '#B3DDB8', '#D3B6D3', '#EFDCA1', '#B4C1D6'];

    const dataW = [disgustW, fearW, angerW, sadnessW, neutralW, surpriseW, joyW];
    const dataR = [disgustR, fearR, angerR, sadnessR, neutralR, surpriseR, joyR];

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
      textStyle: { fontSize: 18, color: '#333', fontWeight: 'normal' }
    });

    // 动态生成 7 个切片网格（Facet Grid），横向拼接
    emotions.forEach((emotion, index) => {
      // 计算每个网格的位置 (左侧留出 12% 给文字标签，剩余 88% 平均分给 7 个网格)
      const leftMargin = 12;
      const gridWidth = 11.2; 
      const gap = 1;
      const currentLeft = leftMargin + index * (gridWidth + gap);

      // 网格配置
      grids.push({
        left: `${currentLeft}%`,
        width: `${gridWidth}%`,
        top: '12%',
        bottom: '8%'
      });

      // 顶部情绪子标题配置
      titles.push({
        text: emotion,
        left: `${currentLeft + gridWidth / 2}%`,
        top: '7%',
        textAlign: 'center',
        textStyle: { fontSize: 15, fontWeight: 'bold', color: '#444' }
      });

      // X轴配置 (底部数值轴)
      xAxes.push({
        gridIndex: index,
        type: 'value',
        splitNumber: 2, // 减少分割线避免拥挤
        axisLabel: { color: '#888', fontSize: 10 },
        splitLine: { lineStyle: { color: '#f3f3f3' } }
      });

      // Y轴配置 (左侧类别轴)
      yAxes.push({
        gridIndex: index,
        type: 'category',
        data: sources,
        inverse: true, // 从上到下显示
        // 只有第一个网格 (Disgust) 显示完整的文字标签，其他网格隐藏，形成表格感
        axisLabel: {
          show: index === 0,
          color: '#333',
          fontWeight: 'bold',
          fontSize: 12,
          padding: [0, 5, 0, 0]
        },
        axisLine: { show: index === 0, lineStyle: { color: '#ccc' } },
        axisTick: { show: false }
      });

      // 填充该网格的 Writer 数据序列
      series.push({
        name: 'Writer',
        type: 'bar',
        xAxisIndex: index,
        yAxisIndex: index,
        data: dataW[index],
        itemStyle: { color: colorWriter[index], borderRadius: [0, 3, 3, 0] },
        label: { show: true, position: 'right', color: '#555', fontSize: 9, formatter: '{c}' },
        barGap: '0%', // 两根柱子紧贴
        barCategoryGap: '35%' // 不同来源之间留出空隙
      });

      // 填充该网格的 Reader 数据序列
      series.push({
        name: 'Reader',
        type: 'bar',
        xAxisIndex: index,
        yAxisIndex: index,
        data: dataR[index],
        itemStyle: { color: colorReader[index], borderRadius: [0, 3, 3, 0] },
        label: { show: true, position: 'right', color: '#555', fontSize: 9, formatter: '{c}' }
      });
    });

    return {
      option: {
        title: titles,
        grid: grids,
        xAxis: xAxes,
        yAxis: yAxes,
        series: series,
        
        // 交互式提示框：鼠标悬停任意柱子时，清晰显示“情绪 - 身份：数值”
        tooltip: {
          trigger: 'item',
          backgroundColor: 'rgba(255, 255, 255, 0.95)',
          textStyle: { color: '#333' },
          formatter: function (params) {
            const emotionName = emotions[params.seriesIndex / 2 | 0];
            return `<b>${params.name}</b><br/>${emotionName} (${params.seriesName}): ${params.value}`;
          }
        },

        // 图例：巧妙地放置在左上角，控制全局的 Writer 和 Reader
        legend: {
          data: ['Writer', 'Reader'],
          top: '2%',
          left: '2%',
          itemWidth: 15,
          itemHeight: 10,
          textStyle: { fontWeight: 'bold', color: '#555' }
        }
      }
    };
  }
};
</script>

<template>
  <div>
    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="22" class="chart-card">
        <div class="scroll-wrapper">
          <v-chart class="chart combined-facet-chart" :option="option" autoresize />
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
/* 增加横向滚动保护，防止在极小屏幕（如手机）上被压缩得看不清 */
.scroll-wrapper {
  width: 100%;
  overflow-x: auto;
}
.chart { 
  /* 强制最小宽度，确保在小屏幕上也能保持 7 个网格的比例，大屏幕则占满 100% */
  min-width: 1000px; 
  width: 100%; 
}
/* 必须赋予足够的高度 (850px)，因为有 13 个数据源，每个源有 2 根柱子 */
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