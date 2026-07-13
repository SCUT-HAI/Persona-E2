<script>
export default {
  data() {
    return {
      bibtex: [
        "@inproceedings{yang2026personae2,",
        "    title={Persona-E$^2$: A Human-Grounded Dataset for Personality-Shaped Emotional Responses to Textual Events},",
        "    author={Yang, Yuqin and Zhou, Haowu and Tu, Haoran and Hui, Zhiwen and Yan, Shiqi and Li, HaoYang and She, Dong and Yao, Xianrong and Gao, Yang and Jin, Zhanpeng},",
        "    booktitle={arXiv preprint arXiv:2604.09162},",
        "    url={https://arxiv.org/abs/2604.09162},",
        "    doi={10.48550/arXiv.2604.09162},",
        "    year={2026}",
        "},",
        "",
        "@inproceedings{yang-etal-2026-persona-e2,",
        "    title = {Persona-E{\u007b}\u007b\u0032\u007d}: A Human-Grounded Dataset for Personality-Shaped Emotional Responses to Textual Events},",
        "    author = {Yang, Yuqin and Zhou, Haowu and Tu, Haoran and Hui, Zhiwen and Yan, Shiqi and Li, HaoYang and She, Dong and Yao, Xianrong and Gao, Yang and Jin, Zhanpeng},",
        "    editor = {Liakata, Maria and Moreira, Viviane P. and Zhang, Jiajun and Jurgens, David},",
        "    booktitle = {Proceedings of the 64th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)},",
        "    month = jul,",
        "    year = {2026},",
        "    address = {San Diego, California, United States},",
        "    publisher = {Association for Computational Linguistics},",
        "    url = {https://aclanthology.org/2026.acl-long.1350/},",
        "    doi = {10.18653/v1/2026.acl-long.1350},",
        "    pages = {29290--29315},",
        "    ISBN = {979-8-89176-390-6},",
        "},",
      ],
    }
  },
  methods: {
    copyVal() {
      let oInput = document.createElement('textarea');
      let text = document.getElementById('bibtex').innerText;
      oInput.value = text;
      document.body.appendChild(oInput);
      oInput.select();
      document.execCommand('Copy');
      this.$message.success('Copy Successfully');
      oInput.remove();
    }
  }
}

</script>

<template>
  <div>
    <el-divider />
      
      <el-row justify="center">
        <h1 class="section-title">BibTeX</h1>
      </el-row>
      
      <el-row justify="center">
        <el-col class='bibtex' :xs="24" :sm="20" :md="14" :lg="12" :xl="12" @click="copyVal()" >
          <div style="text-align: center; color: var(--el-text-color-secondary); margin-top: 20px;">🖱️ Click here to copy BibTex.</div> 
          <el-row>
              <el-scrollbar style="margin: 0px 20px 5px 20px;">
                <pre id="bibtex"><code v-for="b in bibtex">{{ b }}<br/></code></pre>
              </el-scrollbar>
          </el-row>
        </el-col>
      </el-row>

  </div>
</template>

<style scoped>

.scrollbar-flex-content {
  display: flex;
}

/* 卡片属性 */
.bibtex {
  margin: 20px 0px;
  padding-top: 5px;
  box-shadow: var(--el-box-shadow-light); 
  border-radius: 10px;
}

/* 卡片悬浮 */
.bibtex:hover {
  box-shadow: var(--el-box-shadow); 
}

/* 卡片点击 */
.bibtex:active{
  box-shadow: var(--el-box-shadow-lighter); 
}

pre {
  border: none;
  border-radius: 0px;
  padding: 10px;
  background: none;
}

pre code {
  font-size: 18px;
  background: #ffffff;
}



</style>