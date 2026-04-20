<script>
import { use } from 'echarts/core';
import { CanvasRenderer } from 'echarts/renderers';
import { PieChart, BarChart } from 'echarts/charts';
import { TitleComponent, TooltipComponent, LegendComponent, GridComponent } from 'echarts/components';
import VChart from 'vue-echarts';
import { provide } from 'vue';

// 注册所需组件
use([CanvasRenderer, PieChart, BarChart, TitleComponent, TooltipComponent, LegendComponent, GridComponent]);

export default {
  components: { VChart },
  setup() { provide('THEME_KEY', 'light'); },
  data() {
    // 严格映射最新图片中的对比色方案
    const colorNews = '#AA70C6';    // 优雅紫
    const colorSocial = '#D75C5C';  // 砖红色
    const colorLife = '#559DCE';    // 天空蓝
    
    const mutedPalette = [
      '#B584CD', '#C198D4', '#CCABDB', '#D8BFE2', '#E3D3E9',
      '#DC6D6D', '#E17D7D', '#E68E8E', '#EB9E9E', '#EFAFAF', '#F4BFBF', '#F9CFCF', '#FDE0E0', '#FCE8E8',
      '#66A8D3', '#77B4D8', '#88BFDD', '#99CBE2', '#AAD6E7'
    ];

    return {
      option: {
        title: [
          { 
            text: 'Persona-E² Dataset Domain Subcategories & Text Length', 
            left: 'center', 
            top: '2%', 
            // 优化点 1：显著放大标题字体
            textStyle: { fontSize: 26, fontWeight: 'bold', color: '#333' } 
          },
          // 优化点 2：下移柱状图标题位置（从 72% 移至 78%）
          { text: 'News Length', left: '16.66%', top: '78%', textAlign: 'center', textStyle: { fontSize: 14, color: colorNews, fontWeight: 'bold' } },
          { text: 'Social Media Length', left: '50%', top: '78%', textAlign: 'center', textStyle: { fontSize: 14, color: colorSocial, fontWeight: 'bold' } },
          { text: 'Life Exp. Length', left: '83.33%', top: '78%', textAlign: 'center', textStyle: { fontSize: 14, color: colorLife, fontWeight: 'bold' } }
        ],
        
        tooltip: {
          trigger: 'item',
          formatter: function (params) {
            if (params.seriesType === 'pie') {
              return `${params.seriesName} <br/>${params.name}: ${params.value} (${params.percent}%)`;
            } else if (params.seriesType === 'bar') {
              return `${params.seriesName} <br/>${params.name} Text: ${params.value}`;
            }
          },
          backgroundColor: 'rgba(255, 255, 255, 0.95)',
          textStyle: { color: '#333' }
        },

        // 优化点 3：下移柱状图网格位置（从 78% 移至 83%）
        grid: [
          { left: '5%', width: '23.33%', top: '83%', bottom: '4%' },
          { left: '38.33%', width: '23.33%', top: '83%', bottom: '4%' },
          { left: '71.66%', width: '23.33%', top: '83%', bottom: '4%' }
        ],

        xAxis: [
          { type: 'category', data: ['Short', 'Medium', 'Long'], gridIndex: 0, axisLabel: { color: '#666' } },
          { type: 'category', data: ['Short', 'Medium', 'Long'], gridIndex: 1, axisLabel: { color: '#666' } },
          { type: 'category', data: ['Short', 'Medium', 'Long'], gridIndex: 2, axisLabel: { color: '#666' } }
        ],
        yAxis: [
          { type: 'value', gridIndex: 0, splitLine: { show: false }, axisLabel: { show: false } },
          { type: 'value', gridIndex: 1, splitLine: { show: false }, axisLabel: { show: false } },
          { type: 'value', gridIndex: 2, splitLine: { show: false }, axisLabel: { show: false } }
        ],

        series: [
          // ================= [上半部分] 嵌套饼图 =================
          {
            name: 'Main Domain',
            type: 'pie',
            selectedMode: 'single',
            radius: [0, '24%'],
            // 优化点 4：饼图中心点下移（从 37% 移至 43%），增加标题下方间距
            center: ['50%', '43%'], 
            label: { 
              position: 'inner', 
              fontSize: 12, 
              color: '#fff',
              formatter: (params) => params.name.replace(' ', '\n')
            },
            labelLine: { show: false },
            itemStyle: { borderWidth: 1, borderColor: '#fff' },
            data: [
              { value: 506, name: '📰 News', itemStyle: { color: colorNews } },
              { value: 1866, name: '💬 Social Media', itemStyle: { color: colorSocial } },
              { value: 739, name: '🧬 Life Exp.', itemStyle: { color: colorLife } }
            ]
          },
          {
            name: 'Subcategory',
            type: 'pie',
            radius: ['32%', '52%'],
            // 同步调整外圈中心点
            center: ['50%', '43%'],
            color: mutedPalette,
            itemStyle: { borderWidth: 1, borderColor: '#fff' },
            avoidLabelOverlap: true,
            labelLine: { 
              length: 14,    
              length2: 20,  
              smooth: true 
            },
            label: {
              formatter: '{b|{b}}\n{c|{c}}',
              backgroundColor: '#fff',
              borderColor: '#eee',
              borderWidth: 1,
              borderRadius: 4,
              padding: [2, 6],
              rich: {
                b: { color: '#333', fontSize: 11, lineHeight: 16 },
                c: { color: '#888', fontSize: 10, lineHeight: 14 }
              }
            },
            data: [
              { value: 98, name: 'International' }, { value: 56, name: 'Environment' },
              { value: 193, name: 'Health' }, { value: 75, name: 'Education' }, { value: 84, name: 'Economy' },
              { value: 369, name: 'Emotional' }, { value: 7, name: 'Info Sharing' }, { value: 71, name: 'Discussion' },
              { value: 30, name: 'Humor' }, { value: 379, name: 'Self-Record' }, { value: 42, name: 'Technology' },
              { value: 905, name: 'Social' }, { value: 42, name: 'Entertainment' }, { value: 21, name: 'Sports' },
              { value: 309, name: 'Interpersonal' }, { value: 79, name: 'Norm Trans' }, { value: 23, name: 'Reputation' },
              { value: 195, name: 'Routine Daily' }, { value: 133, name: 'Consequences' }
            ]
          },

          // ================= [下半部分] 柱状图 =================
          { 
            name: 'News', type: 'bar', xAxisIndex: 0, yAxisIndex: 0, 
            data: [84, 310, 144], 
            itemStyle: { color: colorNews, borderRadius: [4, 4, 0, 0] },
            label: { show: true, position: 'top', color: '#555', fontSize: 11 },
            emphasis: { focus: 'series' }
          },
          { 
            name: 'Social Media', type: 'bar', xAxisIndex: 1, yAxisIndex: 1, 
            data: [1206, 462, 143], 
            itemStyle: { color: colorSocial, borderRadius: [4, 4, 0, 0] },
            label: { show: true, position: 'top', color: '#555', fontSize: 11 },
            emphasis: { focus: 'series' }
          },
          { 
            name: 'Life Exp.', type: 'bar', xAxisIndex: 2, yAxisIndex: 2, 
            data: [84, 511, 167], 
            itemStyle: { color: colorLife, borderRadius: [4, 4, 0, 0] },
            label: { show: true, position: 'top', color: '#555', fontSize: 11 },
            emphasis: { focus: 'series' }
          }
        ]
      }
    };
  }
};
</script>

<template>
  <div class="chart-section">
    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24" class="chart-card">
        <v-chart class="chart combined-chart" :option="option" autoresize />
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.chart { width: 100%; }
/* 优化点 5：增加整体高度至 850px，提供更多的纵向伸展空间 */
.combined-chart { 
  height: 850px; 
  margin-top: 10px; 
  margin-bottom: 10px; 
}
.chart-card {
  background: #fff; border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.06);
  padding: 20px; transition: transform 0.3s;
}
.chart-card:hover { transform: translateY(-4px); }
</style>