<script setup>
import { ref } from 'vue';

// 当前激活的 Tab
const activeTab = ref('top1');

// 将数据结构转换为扁平对象数组（去除 highlight，让排序更纯粹）
const top1Data = ref([
  { model: 'GPT5.1', prompt: 'General', news: 31.8, social: 18.2, life: 32.4, overall: 29.0 },
  { model: 'GPT5.1', prompt: 'Persona', news: 25.0, social: 18.2, life: 35.3, overall: 27.0 },
  { model: 'GPT5.1', prompt: 'CoT', news: 29.5, social: 27.3, life: 35.3, overall: 31.0 },
  
  { model: 'LLAMA3-8B', prompt: 'General', news: 29.5, social: 9.1, life: 32.4, overall: 26.0 },
  { model: 'LLAMA3-8B', prompt: 'Persona', news: 29.3, social: 4.8, life: 32.4, overall: 25.0 },
  { model: 'LLAMA3-8B', prompt: 'CoT', news: 20.5, social: 13.6, life: 32.4, overall: 23.0 },

  { model: 'QWEN3-8B', prompt: 'General', news: 18.2, social: 23.1, life: 20.3, overall: 20.0 },
  { model: 'QWEN3-8B', prompt: 'Persona', news: 26.9, social: 21.4, life: 33.7, overall: 28.0 },
  { model: 'QWEN3-8B', prompt: 'CoT', news: 25.4, social: 22.7, life: 26.0, overall: 25.0 },

  { model: 'GEMMA3-12B', prompt: 'General', news: 18.2, social: 22.7, life: 35.3, overall: 25.0 },
  { model: 'GEMMA3-12B', prompt: 'Persona', news: 25.0, social: 27.3, life: 32.4, overall: 28.0 },
  { model: 'GEMMA3-12B', prompt: 'CoT', news: 27.3, social: 18.2, life: 29.4, overall: 26.0 },

  { model: 'MINISTRAL3-8B', prompt: 'General', news: 18.2, social: 5.0, life: 36.4, overall: 22.0 },
  { model: 'MINISTRAL3-8B', prompt: 'Persona', news: 13.6, social: 9.1, life: 35.3, overall: 20.0 },
  { model: 'MINISTRAL3-8B', prompt: 'CoT', news: 20.5, social: 4.5, life: 35.3, overall: 22.0 }
]);

const top2Data = ref([
  { model: 'GPT5.1', prompt: 'General', news: 54.5, social: 40.9, life: 47.1, overall: 49.0 },
  { model: 'GPT5.1', prompt: 'Persona', news: 59.1, social: 50.0, life: 55.9, overall: 56.0 },
  { model: 'GPT5.1', prompt: 'CoT', news: 59.1, social: 45.5, life: 55.9, overall: 55.0 },
  
  { model: 'LLAMA3-8B', prompt: 'General', news: 47.7, social: 18.2, life: 50.0, overall: 42.0 },
  { model: 'LLAMA3-8B', prompt: 'Persona', news: 43.9, social: 19.0, life: 47.1, overall: 39.6 },
  { model: 'LLAMA3-8B', prompt: 'CoT', news: 45.5, social: 31.8, life: 44.1, overall: 42.0 },

  { model: 'QWEN3-8B', prompt: 'General', news: 31.3, social: 31.4, life: 39.2, overall: 34.0 },
  { model: 'QWEN3-8B', prompt: 'Persona', news: 33.5, social: 36.4, life: 39.0, overall: 36.0 },
  { model: 'QWEN3-8B', prompt: 'CoT', news: 38.6, social: 39.4, life: 45.1, overall: 41.0 },

  { model: 'GEMMA3-12B', prompt: 'General', news: 36.4, social: 27.3, life: 50.0, overall: 39.0 },
  { model: 'GEMMA3-12B', prompt: 'Persona', news: 47.7, social: 40.9, life: 52.9, overall: 48.0 },
  { model: 'GEMMA3-12B', prompt: 'CoT', news: 56.8, social: 45.5, life: 41.2, overall: 49.0 },

  { model: 'MINISTRAL3-8B', prompt: 'General', news: 40.9, social: 35.0, life: 51.5, overall: 43.3 },
  { model: 'MINISTRAL3-8B', prompt: 'Persona', news: 29.5, social: 36.4, life: 50.0, overall: 38.0 },
  { model: 'MINISTRAL3-8B', prompt: 'CoT', news: 38.6, social: 22.7, life: 50.0, overall: 39.0 }
]);

// 为表格的列设置不同的莫兰迪背景色
const getColumnClass = ({ column }) => {
  if (column.property === 'news') return 'col-news';
  if (column.property === 'social') return 'col-social';
  if (column.property === 'life') return 'col-life';
  if (column.property === 'overall') return 'col-overall';
  return '';
};
</script>

<template>
  <div class="table-section">
    <el-divider />
    
    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="20" :xl="18">
        <h1 class="md-h1">Experimental Results</h1>
        <h2 class="md-h2">Comparison of Different Models (SDS Subset)</h2>
        <p class="md-p">
          The following table summarizes the Top-1 and Top-2 Accuracy across various data sources. 
          <strong>Click on any column header to sort the results.</strong>
        </p>
      </el-col>
    </el-row>

    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="20" :xl="18">
        <el-card class="box-card" shadow="hover">
          
          <el-tabs v-model="activeTab" class="demo-tabs">
            
            <el-tab-pane label="Top-1 Accuracy" name="top1">
              <el-table 
                :data="top1Data" 
                style="width: 100%" 
                :header-cell-class-name="getColumnClass"
                :cell-class-name="getColumnClass"
                :default-sort="{ prop: 'overall', order: 'descending' }"
                border
                stripe
                highlight-current-row
              >
                <el-table-column prop="model" label="Model" min-width="140" fixed="left" sortable>
                  <template #default="scope">
                    <span style="font-weight: bold; color: #444;">{{ scope.row.model }}</span>
                  </template>
                </el-table-column>
                
                <el-table-column prop="prompt" label="Prompt" min-width="110" fixed="left" sortable>
                  <template #default="scope">
                    <el-tag size="small" :type="scope.row.prompt === 'CoT' ? 'primary' : (scope.row.prompt === 'Persona' ? 'success' : 'info')">
                      {{ scope.row.prompt }}
                    </el-tag>
                  </template>
                </el-table-column>
                
                <el-table-column prop="news" label="News" min-width="110" sortable align="center">
                  <template #default="scope">{{ scope.row.news.toFixed(1) }}</template>
                </el-table-column>
                
                <el-table-column prop="social" label="Social Media" min-width="140" sortable align="center">
                  <template #default="scope">{{ scope.row.social.toFixed(1) }}</template>
                </el-table-column>
                
                <el-table-column prop="life" label="Life Exp." min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.life.toFixed(1) }}</template>
                </el-table-column>
                
                <el-table-column prop="overall" label="Overall" min-width="120" sortable align="center">
                  <template #default="scope">
                    <span style="font-weight: 800;">{{ scope.row.overall.toFixed(1) }}</span>
                  </template>
                </el-table-column>
              </el-table>
            </el-tab-pane>

            <el-tab-pane label="Top-2 Accuracy" name="top2">
              <el-table 
                :data="top2Data" 
                style="width: 100%" 
                :header-cell-class-name="getColumnClass"
                :cell-class-name="getColumnClass"
                :default-sort="{ prop: 'overall', order: 'descending' }"
                border
                stripe
                highlight-current-row
              >
                <el-table-column prop="model" label="Model" min-width="140" fixed="left" sortable>
                  <template #default="scope">
                    <span style="font-weight: bold; color: #444;">{{ scope.row.model }}</span>
                  </template>
                </el-table-column>
                
                <el-table-column prop="prompt" label="Prompt" min-width="110" fixed="left" sortable>
                  <template #default="scope">
                    <el-tag size="small" :type="scope.row.prompt === 'CoT' ? 'primary' : (scope.row.prompt === 'Persona' ? 'success' : 'info')">
                      {{ scope.row.prompt }}
                    </el-tag>
                  </template>
                </el-table-column>
                
                <el-table-column prop="news" label="News" min-width="110" sortable align="center">
                  <template #default="scope">{{ scope.row.news.toFixed(1) }}</template>
                </el-table-column>
                
                <el-table-column prop="social" label="Social Media" min-width="140" sortable align="center">
                  <template #default="scope">{{ scope.row.social.toFixed(1) }}</template>
                </el-table-column>
                
                <el-table-column prop="life" label="Life Exp." min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.life.toFixed(1) }}</template>
                </el-table-column>
                
                <el-table-column prop="overall" label="Overall" min-width="120" sortable align="center">
                  <template #default="scope">
                    <span style="font-weight: 800;">{{ scope.row.overall.toFixed(1) }}</span>
                  </template>
                </el-table-column>
              </el-table>
            </el-tab-pane>

          </el-tabs>

        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.md-h1 { font-size: 2.25rem; font-weight: 700; color: #333; text-align: center; margin-top: 1.5rem; margin-bottom: 1rem; font-family: inherit; }
.md-h2 { font-size: 1.5rem; font-weight: 600; color: #333; text-align: center; margin-bottom: 0.75rem; font-family: inherit; }
.md-p { font-size: 1.1rem; line-height: 1.6; color: #555; text-align: center; margin-bottom: 2rem; font-family: inherit; }

.box-card {
  margin-bottom: 40px;
  border-radius: 8px;
}

:deep(.el-tabs__item) {
  font-size: 16px;
  font-weight: bold;
  color: #666;
  padding: 0 30px !important;
}
:deep(.el-tabs__item.is-active) {
  color: #409EFF; 
}

:deep(.el-table) {
  font-family: "Times New Roman", Times, serif;
  font-size: 15px;
}
:deep(.el-table th.el-table__cell) {
  background-color: #f5f7fa;
  color: #333;
  font-weight: bold;
  font-size: 14px;
}

/* 莫兰迪背景色 */
:deep(.col-news) { background-color: rgba(232, 245, 233, 0.4) !important; }
:deep(.col-social) { background-color: rgba(227, 242, 253, 0.4) !important; }
:deep(.col-life) { background-color: rgba(243, 229, 245, 0.4) !important; }
:deep(.col-overall) { background-color: rgba(245, 245, 245, 0.4) !important; }
</style>