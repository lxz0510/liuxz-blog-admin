<template>
  <div class="container-edit">
    <h3>title:</h3>
    <a-input v-model:value="articleTitle" placeholder="title" />
    <h3>article: </h3>
    <WriteMarkdown v-model="articleContent" />

    <a-button class="push-button" @click="handlePushArticle">{{ "Push" }}</a-button>
  </div>

</template>
<script setup>
import { ref } from 'vue'
import axios from 'axios'
import WriteMarkdown from '../components/WriteMarkdown.vue'

const articleTitle = ref("")
const articleContent = ref("# hello")

const handlePushArticle = () => {
  //
  const articleInfo = {
    title: articleTitle.value || "Default Title",
    content: articleContent.value
  }
  console.log(articleInfo)
  // 发起一个post请求
  axios({
    method: 'post',
    url: '',  
    data: {
      firstName: 'Fred',
      lastName: 'Flintstone'
    }
  });
}
</script>
<style>
.container-edit {
  height: 100%
}

.push-button {
  width: 100%;
}
</style>