<script setup>
import page from '../mds/md.mdx';
import DomainPieChart from '../sections/DomainPieChart.vue'
import EmoBarChart from '../sections/EmoBarChart.vue'
import SDS_Distribution from '../sections/SDS_Distribution.vue'
import RQ2_Top1_2Acc from '../sections/RQ2_Top1_2Acc.vue'
import RQ3_Metric from '../sections/RQ3_Metric.vue'
import RQ3_Winrate from '../sections/RQ3_Winrate.vue'

const components = {
  DomainPieChart,
  EmoBarChart,
  SDS_Distribution,
  RQ2_Top1_2Acc,
  RQ3_Metric,
  RQ3_Winrate
}

</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
        <el-col :xs="24" :sm="20" :md="16" :lg="14" :xl="14">
            <page :components="components" />
        </el-col>
    </el-row>

  </div>
</template>