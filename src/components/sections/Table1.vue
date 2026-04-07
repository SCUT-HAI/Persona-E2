<script setup>
const top1Data = [
  { model: 'GPT5.1', news: ['<b>31.8</b>', '25.0', '29.5'], social: ['18.2', '18.2', '<b>27.3</b>'], life: ['32.4', '35.3', '35.3'], overall: ['29.0', '27.0', '<b>31.0</b>'] },
  { model: 'LLAMA3-8B', news: ['29.5', '29.3', '20.5'], social: ['9.1', '4.8', '13.6'], life: ['32.4', '32.4', '32.4'], overall: ['26.0', '25.0', '23.0'] },
  { model: 'QWEN3-8B', news: ['18.2', '26.9', '25.4'], social: ['23.1', '21.4', '22.7'], life: ['20.3', '33.7', '26.0'], overall: ['20.0', '28.0', '25.0'] },
  { model: 'GEMMA3-12B', news: ['18.2', '25.0', '27.3'], social: ['22.7', '<b>27.3</b>', '18.2'], life: ['35.3', '32.4', '29.4'], overall: ['25.0', '28.0', '26.0'] },
  { model: 'MINISTRAL3-8B', news: ['18.2', '13.6', '20.5'], social: ['5.0', '9.1', '4.5'], life: ['<b>36.4</b>', '35.3', '35.3'], overall: ['22.0', '20.0', '22.0'] }
];

const top2Data = [
  { model: 'GPT5.1', news: ['54.5', '59.1', '<b>59.1</b>'], social: ['40.9', '<b>50.0</b>', '45.5'], life: ['47.1', '55.9', '<b>55.9</b>'], overall: ['49.0', '<b>56.0</b>', '55.0'] },
  { model: 'LLAMA3-8B', news: ['47.7', '43.9', '45.5'], social: ['18.2', '19.0', '31.8'], life: ['50.0', '47.1', '44.1'], overall: ['42.0', '39.6', '42.0'] },
  { model: 'QWEN3-8B', news: ['31.3', '33.5', '38.6'], social: ['31.4', '36.4', '39.4'], life: ['39.2', '39.0', '45.1'], overall: ['34.0', '36.0', '41.0'] },
  { model: 'GEMMA3-12B', news: ['36.4', '47.7', '56.8'], social: ['27.3', '40.9', '45.5'], life: ['50.0', '52.9', '41.2'], overall: ['39.0', '48.0', '49.0'] },
  { model: 'MINISTRAL3-8B', news: ['40.9', '29.5', '38.6'], social: ['35.0', '36.4', '22.7'], life: ['51.5', '50.0', '50.0'], overall: ['43.3', '38.0', '39.0'] }
];
</script>

<template>
  <div class="table-section">
    <el-divider />
    
    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="22" :xl="20">
        <h1 class="md-h1">Experimental Results</h1>
        <h2 class="md-h2">Comparison of Different Models (SDS Subset)</h2>
        <p class="md-p">
          The following table summarizes the Top-1 and Top-2 Accuracy across various data sources (News, Social Media, Life-Experience) in the Subjective Divergence Subset (SDS).
        </p>
      </el-col>
    </el-row>

    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="22" :xl="20">
        <div class="table-wrapper">
          <div class="table-responsive">
            <table class="academic-table">
              <thead>
                <tr class="toprule">
                  <th rowspan="2" class="align-middle" style="font-weight: bold;">Metric</th>
                  <th class="text-left align-bottom">Source</th>
                  <th colspan="3" class="cmidrule-header">News</th>
                  <th colspan="3" class="cmidrule-header">Social Media</th>
                  <th colspan="3" class="cmidrule-header">Life Experience</th>
                  <th colspan="3" class="cmidrule-header">Overall</th>
                </tr>
                <tr class="midrule">
                  <th class="text-left align-bottom prompt-label">Prompt</th>
                  <th>General</th><th>Persona</th><th>CoT</th>
                  <th>General</th><th>Persona</th><th>CoT</th>
                  <th>General</th><th>Persona</th><th>CoT</th>
                  <th>General</th><th>Persona</th><th>CoT</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(row, index) in top1Data" :key="'top1-'+index">
                  <td v-if="index === 0" :rowspan="top1Data.length" class="vertical-text metric-label">Top-1 Acc.</td>
                  <td class="text-left model-name">{{ row.model }}</td>
                  <td class="bg-news" v-html="row.news[0]"></td><td class="bg-news" v-html="row.news[1]"></td><td class="bg-news" v-html="row.news[2]"></td>
                  <td class="bg-social" v-html="row.social[0]"></td><td class="bg-social" v-html="row.social[1]"></td><td class="bg-social" v-html="row.social[2]"></td>
                  <td class="bg-life" v-html="row.life[0]"></td><td class="bg-life" v-html="row.life[1]"></td><td class="bg-life" v-html="row.life[2]"></td>
                  <td class="bg-overall" v-html="row.overall[0]"></td><td class="bg-overall" v-html="row.overall[1]"></td><td class="bg-overall" v-html="row.overall[2]"></td>
                </tr>
                <tr class="section-divider"><td colspan="15"></td></tr>
                <tr v-for="(row, index) in top2Data" :key="'top2-'+index">
                  <td v-if="index === 0" :rowspan="top2Data.length" class="vertical-text metric-label">Top-2 Acc.</td>
                  <td class="text-left model-name">{{ row.model }}</td>
                  <td class="bg-news" v-html="row.news[0]"></td><td class="bg-news" v-html="row.news[1]"></td><td class="bg-news" v-html="row.news[2]"></td>
                  <td class="bg-social" v-html="row.social[0]"></td><td class="bg-social" v-html="row.social[1]"></td><td class="bg-social" v-html="row.social[2]"></td>
                  <td class="bg-life" v-html="row.life[0]"></td><td class="bg-life" v-html="row.life[1]"></td><td class="bg-life" v-html="row.life[2]"></td>
                  <td class="bg-overall" v-html="row.overall[0]"></td><td class="bg-overall" v-html="row.overall[1]"></td><td class="bg-overall" v-html="row.overall[2]"></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
/* 模拟 Markdown 字体样式 */
.md-h1 {
  font-size: 2.25rem;
  font-weight: 700;
  color: #333;
  text-align: center;
  margin-top: 1.5rem;
  margin-bottom: 1rem;
  font-family: inherit;
}
.md-h2 {
  font-size: 1.5rem;
  font-weight: 600;
  color: #333;
  text-align: center;
  margin-bottom: 0.75rem;
  font-family: inherit;
}
.md-p {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #555;
  text-align: center;
  margin-bottom: 1.5rem;
  font-family: inherit;
}

.table-wrapper { display: flex; justify-content: center; width: 100%; }
.table-responsive { max-width: 100%; overflow-x: auto; margin-bottom: 40px; }
.academic-table { border-collapse: collapse; text-align: center; font-family: "Times New Roman", Times, serif; font-size: 14px; color: #000; white-space: nowrap; margin: 0 auto; }
.academic-table th, .academic-table td { padding: 6px 6px; vertical-align: middle; }
.toprule th { border-top: 2px solid #000; }
.academic-table tbody tr:last-child td { border-bottom: 2px solid #000; }
.midrule th { border-bottom: 1px solid #000; }
.section-divider td { border-top: 1px solid #000; padding: 2px 0; }
.cmidrule-header { border-bottom: 1px solid #ddd; }
.vertical-text { writing-mode: vertical-rl; transform: rotate(180deg); text-align: center; font-weight: bold; padding: 0 5px !important; background-color: #fff !important; }
.bg-news { background-color: rgba(232, 245, 233, 0.7); }
.bg-social { background-color: rgba(227, 242, 253, 0.7); }
.bg-life { background-color: rgba(243, 229, 245, 0.7); }
.bg-overall { background-color: rgba(245, 245, 245, 0.7); }
.text-left { text-align: left !important; }
.model-name { font-weight: 500; }
</style>