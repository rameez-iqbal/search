<script setup>
import { computed, ref } from "vue";

const Article = ref([
  { title: 'first article', text: 'here is the description about first article' },
  { title: 'second article', text: 'here is the description about second article' },
  { title: 'third article', text: 'here is the description about third article' },
  { title: 'fourth article', text: 'here is the description about fourth article' },
  { title: 'fifth article', text: 'here is the description about fifth article' },
  { title: 'sixth article', text: 'here is the description about sixth article' },
]);

const search = ref('');

const filterArticles = computed(() => {
  return Article.value.filter(item => {
    return (
        item.title.toLowerCase().includes(search.value.toLowerCase()) ||
        item.text.toLowerCase().includes(search.value.toLowerCase())
    );
  });
});
function highlight(text) {
  if (!search.value) return text;
  const searchRegex = new RegExp(`(${search.value})`, 'gi');
  return text.replace(searchRegex, '<mark>$1</mark>');
}
</script>

<template>
  <input type="search" v-model="search" placeholder="Search articles..." />

  <div>
    <div v-for="(article, index) in filterArticles" :key="index">
      <p v-html="highlight(article.title)"></p>
      <p v-html="highlight(article.text)"></p>
    </div>
  </div>
</template>

<style scoped>
input {
  padding: 8px;
  margin-bottom: 16px;
  width: 100%;
  box-sizing: border-box;
}

mark {
  background-color: yellow;
  font-weight: bold;
}
</style>