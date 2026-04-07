<script>
import Title from './sections/Title.vue'
import Abstract from './sections/Abstract.vue'
import Markdown from './sections/Markdown.vue'
import BibTeX from './sections/BibTeX.vue'
import Carousel from './sections/Carousel.vue'
import Video from './sections/Video.vue'
import ImageSlider from './sections/ImageSlider.vue'
import ImageSliderInner from './sections/ImageSliderInner.vue'
import ImageSelector from './sections/ImageSelector.vue'
import Echart from './sections/Echart.vue'
import EmoBarChart from './sections/EmoBarChart.vue'
import DomainPieChart from './sections/DomainPieChart.vue'
import Table from './sections/Table.vue'
import Table1 from './sections/Table1.vue'
import Table2 from './sections/Table2.vue'
import Collapse from './sections/Collapse.vue'
import SeletionForComparison from './sections/SeletionForComparison.vue'
import Comment from './sections/Comment.vue'
import Latex from './sections/Latex.vue'
import Model3D from './sections/Model3D.vue'
import GaussianSplats3D from './sections/GaussianSplats3D.vue'
export default {
  components: {
    Title,
    Abstract,
    Markdown,
    BibTeX,
    Carousel,
    Video,
    ImageSlider,
    ImageSliderInner,
    ImageSelector,
    Echart,
    // 2. 在这里注册刚刚引入的组件
    EmoBarChart,
    DomainPieChart,
    Collapse,
    Table,
    Table1,
    Table2,
    SeletionForComparison,
    Comment,
    Latex,
    Model3D,
    GaussianSplats3D
  }
}
</script>

<template>
  <Title/>
  <Abstract/>
  <Markdown/>
  <Table1/>
  <Table2/>
  <Echart/>
  <EmoBarChart/>
  <DomainPieChart/>

  <BibTeX/>
  </template>