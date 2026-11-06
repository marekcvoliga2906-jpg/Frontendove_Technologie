<script setup>
import { ref } from 'vue';

const articles = ref([
{ id: 1, title: 'My journey with Vue', text: 'My journey with Vue is not very enjoyable.' },
{ id: 2, title: 'Blogging with Vue', text: 'Why am I only creating blogs?' },
{ id: 3, title: 'Why Vue is so fun', text: 'It is not fun lol.' }]
);
</script>
<template>
<div class="about">
<h1 style="margin-bottom: 30px;">This is my Blog page</h1>
<div style="padding-bottom: 10px;" 
v-for="article in articles" :key="article.id">
<RouterLink 
:to="'blog/' + article.title">{{ article.title }}</RouterLink>
</div>
</div>
</template>

<style>
@media (min-width: 1024px) {
  .blog {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
