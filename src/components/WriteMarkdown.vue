<template>
  <div id="editor">
    <textarea :value="modelValue" @input="update"></textarea>
    <div v-html="compiledMarkdown" class="compiledMarkdown"></div>
  </div>
</template>
<script setup>
import { ref, computed } from 'vue'
import { marked } from 'marked';
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

const input = ref("# hello")

const update = (e) => {
  emit('update:modelValue', e.target.value)
}
const compiledMarkdown = computed(() => {
  return marked(props.modelValue, { sanitize: true })
})
</script>
<style>
#editor {
  border: 1px solid #40a9ff;
  margin: 0;
  height: 80%;
  font-family: "Helvetica Neue", Arial, sans-serif;
  color: #333;
}

textarea,
#editor div {
  display: inline-block;
  width: 49%;
  height: 100%;
  vertical-align: top;
  box-sizing: border-box;
  padding: 0 20px;
}

textarea {
  border: none;
  border-right: 1px solid #ccc;
  resize: none;
  outline: none;
  background-color: #f6f6f6;
  font-size: 14px;
  font-family: "Monaco", courier, monospace;
  padding: 20px;
}

.compiledMarkdown {
  overflow: auto
}

code {
  color: #f66;
}
</style>