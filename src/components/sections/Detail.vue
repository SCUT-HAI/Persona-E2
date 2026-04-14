<script setup>
// 使用 Element Plus 的 el-collapse，无需额外写 JS 逻辑
</script>

<template>
  <div class="collapse-section">
    <el-divider />

    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="24" :lg="20" :xl="18">
        <h1 class="md-h1">Evaluation Metrics Details</h1>
      </el-col>
    </el-row>

    <el-row justify="center">
      <el-col :xs="24" :sm="22" :md="20" :lg="16" :xl="14">
        
        <el-collapse model-value="1" class="custom-collapse" accordion>

          <el-collapse-item title="Cognitive Consistency" name="1">
            <div class="collapse-content">
              Assesses whether the rationale aligns with the specific values and behavioral patterns of the assigned persona. A rationale that exhibits thinking patterns divergent from those of the specified persona is considered of poor quality.
            </div>
          </el-collapse-item>

          <el-collapse-item title="Reasoning Plausibility" name="2">
            <div class="collapse-content">
              Evaluates the logical coherence of the causal chain from the event to the elicited emotion. A post-hoc justification that merely reverse-engineers the given emotion is considered poor quality.
            </div>
          </el-collapse-item>

          <el-collapse-item title="Emotional Specificity" name="3">
            <div class="collapse-content">
              Measures how precisely the rationale is tailored to explain the specific target emotion. A vague rationale that could explain any emotional response is considered poor quality.
            </div>
          </el-collapse-item>

        </el-collapse>
      </el-col>
    </el-row>

  </div>
</template>

<style scoped>
/* 继承前面组件的标题样式 */
.md-h1 { 
  font-size: 2.25rem; 
  font-weight: 700; 
  color: #333; 
  text-align: center; 
  margin-top: 1.5rem; 
  margin-bottom: 2rem; 
  font-family: inherit; 
}

.collapse-section {
  margin-bottom: 50px;
}

/* 优化 Collapse 容器，增加微弱阴影和圆角，匹配学术高级感 */
.custom-collapse {
  border-top: none;
  border-bottom: none;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.04);
  border-radius: 8px;
  background: #fff;
  padding: 10px 20px;
}

/* 深度修改 Element Plus 默认的表头样式 */
:deep(.el-collapse-item__header) {
  font-size: 1.15rem;
  font-weight: 600;
  color: #333;
  border-bottom: 1px solid #f0f2f5; /* 更柔和的分割线 */
}

/* 展开时的标题颜色，使用之前表格的学术蓝 */
:deep(.el-collapse-item__header.is-active) {
  color: #4C5F7F; 
}

/* 去掉最后一个 item 的底边框 */
:deep(.el-collapse-item:last-child .el-collapse-item__header) {
  border-bottom: none;
}
:deep(.el-collapse-item__wrap) {
  border-bottom: none;
}

/* 内部正文样式：使用衬线字体（Times New Roman）提升学术阅读体验 */
.collapse-content {
  font-size: 1.05rem;
  line-height: 1.6;
  color: #555;
  padding-top: 10px;
  padding-bottom: 15px;
  font-family: "Times New Roman", Times, serif; 
}
</style>