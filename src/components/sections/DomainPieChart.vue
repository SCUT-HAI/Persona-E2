<script>
import { use } from 'echarts/core';
import { CanvasRenderer } from 'echarts/renderers';
import { PieChart, BarChart } from 'echarts/charts';
import { TitleComponent, TooltipComponent, LegendComponent, GridComponent } from 'echarts/components';
import VChart from 'vue-echarts';
import { provide } from 'vue';

// 注册所需组件，包括饼图、柱状图和网格布局
use([CanvasRenderer, PieChart, BarChart, TitleComponent, TooltipComponent, LegendComponent, GridComponent]);

export default {
  components: { VChart },
  setup() { provide('THEME_KEY', 'light'); },
  data() {
    // 严格映射论文中的莫兰迪色系
    const slateBlue = '#4C5F7F';   // News
    const softCoral = '#E6A280';   // Social Media
    const softNeutral = '#AFAFAF'; // Life Exp
    
    // 外圈渐变色系
    const mutedPalette = [
      '#6C7B9F', '#7A8AA9', '#93A4C0', '#ACBCD6', '#C5D4EC', 
      '#EFBFA7', '#F3CCC0', '#F7D9D9', '#FBE5F2', '#EED4A6', 
      '#DDBB99', '#E8B898', '#F0C8B8', '#F5D8C8',
      '#B0C1D0', '#C2D1E0', '#D4E1F0', '#E6F1FF', '#D9E5F2'
    ];

    return {
      option: {
        // 1. 标题配置（支持数组格式，用于在图表内不同位置放置子标题）
        title: [
          { 
            text: 'Persona-E² Dataset Domain Subcategories & Text Length', 
            left: 'center', 
            top: '2%', 
            textStyle: { fontSize: 18, fontWeight: 'normal', color: '#333' } 
          },
          // 下方三个柱状图的专属标题
          { text: 'News Length', left: '16.66%', top: '70%', textAlign: 'center', textStyle: { fontSize: 14, color: slateBlue, fontWeight: 'bold' } },
          { text: 'Social Media Length', left: '50%', top: '70%', textAlign: 'center', textStyle: { fontSize: 14, color: softCoral, fontWeight: 'bold' } },
          { text: 'Life Exp. Length', left: '83.33%', top: '70%', textAlign: 'center', textStyle: { fontSize: 14, color: softNeutral, fontWeight: 'bold' } }
        ],
        
        // 2. 交互式提示框（智能判断是饼图还是柱状图）
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

        // 3. 网格划分（在底部划分出左、中、右三个区域给柱状图）
        grid: [
          { left: '5%', width: '23.33%', top: '76%', bottom: '5%' },
          { left: '38.33%', width: '23.33%', top: '76%', bottom: '5%' },
          { left: '71.66%', width: '23.33%', top: '76%', bottom: '5%' }
        ],

        // 4. 为每个网格配置独立的 X/Y 轴
        xAxis: [
          { type: 'category', data: ['Short', 'Medium', 'Long'], gridIndex: 0, axisLabel: { color: '#666', interval: 0 } },
          { type: 'category', data: ['Short', 'Medium', 'Long'], gridIndex: 1, axisLabel: { color: '#666', interval: 0 } },
          { type: 'category', data: ['Short', 'Medium', 'Long'], gridIndex: 2, axisLabel: { color: '#666', interval: 0 } }
        ],
        yAxis: [
          { type: 'value', gridIndex: 0, splitLine: { lineStyle: { type: 'dashed', color: '#eee' } }, axisLabel: { show: false } },
          { type: 'value', gridIndex: 1, splitLine: { lineStyle: { type: 'dashed', color: '#eee' } }, axisLabel: { show: false } },
          { type: 'value', gridIndex: 2, splitLine: { lineStyle: { type: 'dashed', color: '#eee' } }, axisLabel: { show: false } }
        ],

        // 5. 数据序列（整合了上方的饼图和下方的柱状图）
        series: [
          // ================= [上半部分] 嵌套饼图 =================
          {
            name: 'Main Domain',
            type: 'pie',
            selectedMode: 'single',
            radius: [0, '22%'],
            center: ['50%', '38%'], // 定位在偏上方的位置
            label: { position: 'inner', fontSize: 13, color: '#fff' },
            labelLine: { show: false },
            itemStyle: { borderWidth: 1, borderColor: '#fff' },
            data: [
              { value: 506, name: '📰 News', itemStyle: { color: slateBlue } },
              { value: 1866, name: '💬 Social Media', itemStyle: { color: softCoral } },
              { value: 739, name: '🧬 Life Exp.', itemStyle: { color: softNeutral } }
            ]
          },
          {
            name: 'Subcategory',
            type: 'pie',
            radius: ['30%', '50%'],
            center: ['50%', '38%'],
            color: mutedPalette,
            itemStyle: { borderWidth: 1, borderColor: '#fff' },
            avoidLabelOverlap: true,
            labelLine: { length: 15, length2: 25, smooth: true }, // 平滑牵引线，彻底解决文字重叠
            label: {
              formatter: '{b|{b}}\n{c|{c}}',
              backgroundColor: '#fff',
              borderColor: '#eee',
              borderWidth: 1,
              borderRadius: 4,
              padding: [4, 8],
              rich: {
                b: { color: '#333', fontSize: 12, fontWeight: 'normal', lineHeight: 20, padding: [0, 2] },
                c: { color: '#666', fontSize: 11, lineHeight: 18, padding: [0, 2] }
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

          // ================= [下半部分] 底部三个交互式柱状图 =================
          { 
            name: 'News', type: 'bar', xAxisIndex: 0, yAxisIndex: 0, 
            data: [84, 310, 144], 
            itemStyle: { color: slateBlue, borderRadius: [4, 4, 0, 0] },
            label: { show: true, position: 'top', color: '#555', fontWeight: 'bold' }, // 柱子顶部显示具体数值
            emphasis: { focus: 'series' }
          },
          { 
            name: 'Social Media', type: 'bar', xAxisIndex: 1, yAxisIndex: 1, 
            data: [1206, 462, 143], 
            itemStyle: { color: softCoral, borderRadius: [4, 4, 0, 0] },
            label: { show: true, position: 'top', color: '#555', fontWeight: 'bold' },
            emphasis: { focus: 'series' }
          },
          { 
            name: 'Life Exp.', type: 'bar', xAxisIndex: 2, yAxisIndex: 2, 
            data: [84, 511, 167], 
            itemStyle: { color: softNeutral, borderRadius: [4, 4, 0, 0] },
            label: { show: true, position: 'top', color: '#555', fontWeight: 'bold' },
            emphasis: { focus: 'series' }
          }
        ]
      }
    };
  }
};
</script>

<template>
  <div>
    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="22" :lg="20" :xl="18" class="chart-card">
        <v-chart class="chart combined-chart" :option="option" autoresize />
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.chart { 
  width: 100%; 
}
/* 重点修改：图表高度加大，以便容纳上下两层结构（饼图+柱图） */
.combined-chart { 
  height: 750px; 
  margin-top: 10px; 
  margin-bottom: 20px; 
}
.chart-card {
  background: #fff; 
  border-radius: 8px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.05);
  padding: 15px; 
  transition: all 0.3s ease;
}
.chart-card:hover { 
  box-shadow: 0 4px 20px 0 rgba(0, 0, 0, 0.08); 
}
</style>