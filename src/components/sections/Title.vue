<script lang="ts" setup>

import { ElIcon } from 'element-plus'
// 以下图标均来自 Element Plus 官方图标库 @element-plus/icons-vue
// 查看全部可用图标：
// 1. 官方文档 https://element-plus.org/zh-CN/component/icon
// 2. 直接浏览源码 https://github.com/element-plus/element-plus-icons-vue/tree/main/packages
// 3. 本地 node_modules/@element-plus/icons-vue/dist/index.d.ts 中查看导出列表
import { Document, Files, MagicStick, Picture, DataAnalysis, Film, DataBoard, Tools, Collection } from '@element-plus/icons-vue'

// logo地址，没有则置为""即可
const logo = "./icon/Web-logo.png"

// 标题
const title = 'Persona-E²'

// 标题颜色
const title_color = '#000000'

// 标题补充，没有则置为''即可
const title_supp = ': A Human-Grounded Dataset for Personality-Shaped Emotional Responses to Textual Events'

// 标题补充颜色
const title_supp_color = '#42B883'

// 按钮颜色
const btn_color = '#444444'

// 作者清单（包含作者姓名、头像、主页、地址序号）
const authors = [
  {
    name: "Yuqin Yang",
    icon: "./icon/photoYang.jpg",
    homepage: "https://github.com/CRIS-YANGYQ",
    address_flag: "1,2"
  },
  {
    name: "Haowu Zhou",
    icon: "./icon/photoZhou.png",
    homepage: "https://github.com/zhouhaowu",
    address_flag: "1"
  },
  {
    name: "Haoran Tu",
    icon: "./icon/photoTu.jpg",
    homepage: "https://github.com/PeterTuhaoran",
    address_flag: "1"
  },
  {
    name: "Zhiwen Hui",
    icon: "./icon/photoHui.jpg",
    homepage: "https://github.com/HZW-1",
    address_flag: "1"
  },
  {
    name: "Shiqi Yan",
    icon: "./icon/photoYan.png",
    homepage: "https://github.com/ldylle",
    address_flag: "1"
  },
  {
    name: "HaoYang Li",
    icon: "./icon/photoLi.png",
    homepage: "https://github.com/L3033",
    address_flag: "1"
  },
  {
    name: "Dong She",
    icon: "./icon/photoSheDong.jpg",
    homepage: "https://github.com/Affective-AI",
    address_flag: "1,2"
  },
  {
    name: "Xianrong Yao",
    icon: "./icon/photoYao.png",
    homepage: "#",
    address_flag: "1,2"
  },
  {
    name: "Yang Gao",
    icon: "./icon/photoGao.jpg",
    homepage: "https://ygao36buffalo.github.io/truebluegy.github.io/",
    address_flag: "1,2,*"
  },
  {
    name: "Zhanpeng Jin",
    icon: "./icon/photoJin.jpg",
    homepage: "https://www2.scut.edu.cn/gzic_en/2025/0711/c44985a602804/page.htm",
    address_flag: "1,2,*"
  },
]

// 地址清单（包含地址名称、头像、主页、地址序号）
const addresses = [
  {
    address_flag: "1",
    name: "South China University of Technology",
    icon: "./icon/scut-logo.png",
    homepage: "https://www.scut.edu.cn/"
  },
  {
    address_flag: "2",
    name: "HAI Lab",
    icon: "./icon/Web-logo.png",
    homepage: "https://scuthcc.top/"
  },
]

// 共一和通讯提示
const con_and_corresponding_author = 
  "*: Corresponding Author."

// 最新消息
const news = "🔥 [2026-03-19] Persona-E² project page is launched."

// 强调内容
const emphases = [
  "🎉 [ACL 2026] Main Conference",
  "🥰 Persona-driven Event and Emotion Relationship",
  "Explore the impact of persona on emotional responses to events",
  "Large-scale dataset with expert annotations",
  "Connect us: ftyuqin_yang@mail.scut.edu.cn"
]

// 提供引导资料链接
const buttons = [
  {
    disabled: false,
    name: "Paper",
    link: "https://arxiv.org/abs/2604.09162",
    component: Document,
  },
  {
    disabled: false,
    name: "Label Toolkit",
    link: "https://github.com/CRIS-YANGYQ/LabelText",
    component: Tools,
  },
  {
    disabled: false,
    name: "Project Page",
    link: "https://scuthcc.top/Persona-E2/",
    component: Files,
  },
  {// Kaggle Dataset
    disabled: false,
    name: "Kaggle",
    link: "https://www.kaggle.com/datasets/crisyang777/peronsa-e-personality-shaped-emotion-dataset",
    component: Collection,
  },
  {// Huggingface Dataset
    disabled: false,
    name: "Huggingface",
    link: "https://huggingface.co/datasets/CRIS-YANGYQ/Persona-E2",
    component: Collection,
  },
  {
    disabled: true,
    name: "Demo",
    component: MagicStick,
  },
  {
    disabled: true,
    name: "Poster",
    component: Picture,
  },
  {
    disabled: true,
    name: "Slide",
    component: DataAnalysis,
  },
  {
    disabled: true,
    name: "Video",
    // link: "",
    component: Film,
  },
  {
    disabled: true,
    name: "Video (Tutorial)",
    component: Film,
  },
]

</script>

<template>
  <div>

    <!-- 最新消息提示 -->
    <el-row justify="center">
      <el-col :span="24">
        <el-alert title="🔍 Feel free to contact us if you have any questions." type="success" />
      </el-col>
    </el-row>

    <!-- 文章logo -->
    <el-row v-if="logo" justify="center">
      <el-image :src="logo" class="logo" fit="cover" />
    </el-row>

    <!-- 文章标题 -->
    <el-row justify="center">
      <el-col :span="20">
        <h1 class="paper-title">
          <span v-if="title" :style="{color:title_color}"> {{ title }}</span>
          <span v-if="title_supp" :style="{color:title_supp_color}"> {{ title_supp }}</span>
        </h1>
      </el-col>
    </el-row>

    <el-row justify="center" class="badge-row">
      <img class="badge-img" src="https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-blue.svg" alt="License" />
      <img class="badge-img" src="https://img.shields.io/badge/Annotations-111k-success.svg" alt="Annotations" />
      <img class="badge-img" src="https://img.shields.io/badge/Task-Emotion%20Classification-orange.svg" alt="Task" />
      <a href="https://www.kaggle.com/datasets/crisyang777/peronsa-e-personality-shaped-emotion-dataset" target="_blank" rel="noopener noreferrer">
        <img class="badge-img" src="https://img.shields.io/badge/Kaggle-Dataset-20BEFF?logo=kaggle&logoColor=white" alt="Kaggle" />
      </a>
      <img class="badge-img" src="https://img.shields.io/badge/Huggingface-Coming%20soon-lightgrey.svg" alt="Huggingface Coming Soon" />
      <a href="https://arxiv.org/abs/2604.09162" target="_blank" rel="noopener noreferrer">
        <img class="badge-img" src="https://img.shields.io/badge/arXiv-2604.09162-b31b1b?logo=arxiv&logoColor=white" alt="Arxiv" />
      </a>
      <img class="badge-img" src="https://img.shields.io/badge/ACL%202026-Coming%20soon-lightgrey.svg" alt="ACL 2026 Coming Soon" />
    </el-row>

    <!-- 作者名单 -->
    <el-row justify="center">
      <a :href=author.homepage v-for="author in authors">
        <el-button class="title-button" type="primary" text>
          <el-avatar v-if="author.icon" :size="40" :src="author.icon" />
          <span class="author">
            {{ author.name }}<sup v-if="author.address_flag" class="name_sup">{{ author.address_flag }}</sup>
          </span>
        </el-button>
      </a>
    </el-row>

    <!-- 共一和通讯提示内容 -->
    <el-row justify="center" class="con-cor">
        {{ con_and_corresponding_author }}
    </el-row>

    <!-- 地址名单 -->
    <el-row justify="center">
      <a :href=address.homepage v-for="address in addresses">
        <el-button class="title-button" type="primary" text>
          <el-avatar v-if="address.icon" :size="40" :src="address.icon" />
          <span class="address">
            <sup v-if="address.address_flag" class="address_sup">{{ address.address_flag }}</sup>{{ address.name }}
          </span>
        </el-button>
      </a>
    </el-row>

    <!-- 强调内容 -->
    <el-row justify="center" class="emphasis" v-for="emphasis in emphases">
        {{ emphasis }}
    </el-row>

    <!-- 提供引导按钮 -->
    <el-row justify="center" style="margin-bottom: 20px;">
      <el-col :span="20">
        <el-row justify="center">
          <a :href=button.link v-for="button in buttons">
            <el-button class="guidance-button" size="default" :color="btn_color" :disabled="button.disabled" round>
              <el-icon :size="18">
                <component :is="button.component" />
              </el-icon>
              <span class="btn-text">{{ button.name }}</span>
            </el-button>
          </a>
        </el-row>
      </el-col>
    </el-row>

  </div>
</template>

<style scoped>

/* 文章标题字体、字间距、居中排布、字号 */
.paper-title {
  font-family: "MyFont", Verdana, sans-serif;
  letter-spacing: 2px;
  font-size: 42px;
  margin: 32px;
  text-align: center;
}

/* 标题下方徽章 */
.badge-row {
  margin: -8px 0 14px;
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.badge-img {
  height: 20px;
}

/* 姓名和地址按钮 */
.title-button {
  margin: 10px 3px;
}

/* 姓名和地址按钮光标悬浮 */
.title-button:hover {
  margin: 10px 8px;
}

/* 引导材料按钮 */
.guidance-button {
  margin: 8px 5px;
  box-shadow: #d8d8d8 1px 1px 1px 1px;
}

/* 姓名属性 */
.author {
  font-size: 18px;
  margin-left: 3px;
}

/* 姓名上标属性 */
.name_sup {
  color: #606266; 
  margin-left: 3px;
}

/* 地址属性 */
.address {
  font-size: 18px;
}

/* 地址上标属性 */
.address_sup {
  color: #606266; 
  margin-right: 1px;
}

/* 头像属性 */
.el-avatar {
  margin-right: 6px;
  box-shadow: #b7b7b7 0px 0px 3px 1px;
}

/* 共一和通讯文字属性 */
.con-cor {
  font-family: Arial;
  font-size: 14px;
  margin: 18px 0px;
  text-align: center;
}

/* 强调信息属性 */
.emphasis {
  color: chocolate;
  font-weight: bold;
  margin: 8px;
  font-size: 22px;
  text-align: center;
}

/* 引导材料按钮文字属性 */
.btn-text {
  font-size: 18px;
  color: #ffffff;
}

.el-alert {
  margin: 10px 0 0;
}

.el-alert:first-child {
  margin: 0;
}

.logo {
  width: 150px; 
  height: 150px;
  border-radius: 50%;
  box-shadow: #ced3dc 0px 0px 3px 2px;
  margin-top: 40px;
}

/* 手机端链接样式处理 */
a:-webkit-any-link {
  text-decoration: none;
}

/* 取消鼠标焦点悬浮在链接上的颜色装饰 */
a:hover {
  color: inherit;
  border-bottom: none;
}

/* 链接装饰，取消下划线和链接颜色 */
a {
	text-decoration: None;
	color: inherit;
}

</style>