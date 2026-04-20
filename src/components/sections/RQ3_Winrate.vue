<script setup>
import { ref } from 'vue';

// 当前激活的 Tab，默认显示 Consistency
const activeTab = ref('consistency');

// 完整的认知合理性跑分数据
const tableData = ref([
  { model: 'GPT5.1', cons_bl: 4.7, cons_mbti: 16.5, cons_bfi: 78.8, plaus_bl: 13.8, plaus_mbti: 15.8, plaus_bfi: 70.4, spec_bl: 17.6, spec_mbti: 13.5, spec_bfi: 68.9 },
  { model: 'LLAMA3', cons_bl: 9.4, cons_mbti: 19.8, cons_bfi: 70.8, plaus_bl: 21.5, plaus_mbti: 23.1, plaus_bfi: 55.4, spec_bl: 20.5, spec_mbti: 18.2, spec_bfi: 61.3 },
  { model: 'QWEN3', cons_bl: 10.4, cons_mbti: 19.4, cons_bfi: 70.2, plaus_bl: 19.7, plaus_mbti: 20.4, plaus_bfi: 59.9, spec_bl: 23.7, spec_mbti: 19.4, spec_bfi: 56.9 },
  { model: 'GEMMA3', cons_bl: 14.8, cons_mbti: 17.4, cons_bfi: 67.8, plaus_bl: 21.8, plaus_mbti: 15.1, plaus_bfi: 63.1, spec_bl: 19.5, spec_mbti: 15.5, spec_bfi: 65.0 },
  { model: 'MINISTRAL3', cons_bl: 12.5, cons_mbti: 15.5, cons_bfi: 72.0, plaus_bl: 21.6, plaus_mbti: 19.5, plaus_bfi: 58.9, spec_bl: 22.0, spec_mbti: 12.5, spec_bfi: 65.5 }
]);

// 分别为三个 Tab 定义列的背景色渲染逻辑 (除了 Model 列外，其余列加上对应的背景色)
const getConsistencyClass = ({ columnIndex }) => columnIndex > 0 ? 'col-consistency' : '';
const getPlausibilityClass = ({ columnIndex }) => columnIndex > 0 ? 'col-plausibility' : '';
const getSpecificityClass = ({ columnIndex }) => columnIndex > 0 ? 'col-specificity' : '';
</script>

<template>
  <div class="table-section">
    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="20" :xl="18">
        <p class="md-p">
          We evaluated the cognitive plausibility of the psychological reasoning process.
          <strong>Click on any metric header to sort the models.</strong>
        </p>
        
        <el-tabs v-model="activeTab" class="academic-tabs" stretch>
          
          <el-tab-pane label="Consistency" name="consistency">
            <div class="table-responsive">
              <el-table 
                :data="tableData" 
                style="width: 100%" 
                :header-cell-class-name="getConsistencyClass"
                :cell-class-name="getConsistencyClass"
                :default-sort="{ prop: 'cons_bfi', order: 'descending' }"
                border
                stripe
                highlight-current-row
              >
                <el-table-column prop="model" label="Model" min-width="160" fixed="left" sortable>
                  <template #default="scope">
                    <span class="model-name">{{ scope.row.model }}</span>
                  </template>
                </el-table-column>
                <el-table-column prop="cons_bl" label="BL" min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.cons_bl.toFixed(1) }}</template>
                </el-table-column>
                <el-table-column prop="cons_mbti" label="MBTI" min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.cons_mbti.toFixed(1) }}</template>
                </el-table-column>
                <el-table-column prop="cons_bfi" label="BFI" min-width="120" sortable align="center">
                  <template #default="scope">
                    <span class="highlight-bold">{{ scope.row.cons_bfi.toFixed(1) }}</span>
                  </template>
                </el-table-column>
              </el-table>
            </div>
          </el-tab-pane>

          <el-tab-pane label="Plausibility" name="plausibility">
            <div class="table-responsive">
              <el-table 
                :data="tableData" 
                style="width: 100%" 
                :header-cell-class-name="getPlausibilityClass"
                :cell-class-name="getPlausibilityClass"
                :default-sort="{ prop: 'plaus_bfi', order: 'descending' }"
                border
                stripe
                highlight-current-row
              >
                <el-table-column prop="model" label="Model" min-width="160" fixed="left" sortable>
                  <template #default="scope">
                    <span class="model-name">{{ scope.row.model }}</span>
                  </template>
                </el-table-column>
                <el-table-column prop="plaus_bl" label="BL" min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.plaus_bl.toFixed(1) }}</template>
                </el-table-column>
                <el-table-column prop="plaus_mbti" label="MBTI" min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.plaus_mbti.toFixed(1) }}</template>
                </el-table-column>
                <el-table-column prop="plaus_bfi" label="BFI" min-width="120" sortable align="center">
                  <template #default="scope">
                    <span class="highlight-bold">{{ scope.row.plaus_bfi.toFixed(1) }}</span>
                  </template>
                </el-table-column>
              </el-table>
            </div>
          </el-tab-pane>

          <el-tab-pane label="Specificity" name="specificity">
            <div class="table-responsive">
              <el-table 
                :data="tableData" 
                style="width: 100%" 
                :header-cell-class-name="getSpecificityClass"
                :cell-class-name="getSpecificityClass"
                :default-sort="{ prop: 'spec_bfi', order: 'descending' }"
                border
                stripe
                highlight-current-row
              >
                <el-table-column prop="model" label="Model" min-width="160" fixed="left" sortable>
                  <template #default="scope">
                    <span class="model-name">{{ scope.row.model }}</span>
                  </template>
                </el-table-column>
                <el-table-column prop="spec_bl" label="BL" min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.spec_bl.toFixed(1) }}</template>
                </el-table-column>
                <el-table-column prop="spec_mbti" label="MBTI" min-width="120" sortable align="center">
                  <template #default="scope">{{ scope.row.spec_mbti.toFixed(1) }}</template>
                </el-table-column>
                <el-table-column prop="spec_bfi" label="BFI" min-width="120" sortable align="center">
                  <template #default="scope">
                    <span class="highlight-bold">{{ scope.row.spec_bfi.toFixed(1) }}</span>
                  </template>
                </el-table-column>
              </el-table>
            </div>
          </el-tab-pane>

        </el-tabs>

      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
/* 继承 Markdown 的文字风格 */
.md-h2 { font-size: 1.5rem; font-weight: 600; color: #333; text-align: center; margin-bottom: 0.75rem; font-family: inherit; }
.md-p { font-size: 1.1rem; line-height: 1.6; color: #555; text-align: center; margin-bottom: 2rem; font-family: inherit; }

.table-section { margin-bottom: 40px; }
.table-responsive { max-width: 100%; overflow-x: auto; padding-top: 10px; }

/* 优化 Tabs 的外观，增加学术高级感 (与 Table1 保持一致) */
.academic-tabs {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.05);
  padding: 10px 20px 20px 20px;
}
:deep(.el-tabs__item) {
  font-size: 16px;
  font-weight: bold;
  color: #666;
}
:deep(.el-tabs__item.is-active) {
  color: #4C5F7F; /* 学术主题蓝 */
}
:deep(.el-tabs__active-bar) {
  background-color: #4C5F7F;
}

/* 覆盖 Element Plus 表格默认样式 */
:deep(.el-table) {
  font-family: "Times New Roman", Times, serif; /* 保留学术字体 */
  font-size: 15px;
}

:deep(.el-table th.el-table__cell) {
  color: #222;
  font-weight: bold;
  font-size: 15px;
}

/* 注入原图的莫兰迪色系背景 */
:deep(.col-consistency) { background-color: rgba(234, 245, 252, 0.5) !important; }
:deep(.col-plausibility) { background-color: rgba(253, 243, 235, 0.6) !important; }
:deep(.col-specificity) { background-color: rgba(238, 251, 240, 0.6) !important; }

/* 模型名称：使用小型大写字母（学术风格）或加粗 */
.model-name {
  font-weight: 600;
  color: #333;
  font-variant: small-caps;
  font-size: 16px;
}

/* BFI 这一列的数据加粗高亮 */
.highlight-bold {
  font-weight: 800;
  color: #000;
}
</style>