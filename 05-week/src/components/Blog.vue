<script setup>
import { ref } from 'vue'
import Article from './Article.vue'

const articles = ref([
  {
    id: 1,
    title: 'Prvý článok: Úvod do Vue.js',
    text: 'Vue.js je progresívny JavaScriptový framework pre tvorbu používateľských rozhraní.'
  },
  {
    id: 2,
    title: 'Druhý článok: Prečo používať komponenty?',
    text: 'Komponenty nám umožňujú rozdeliť používateľské rozhranie na nezávislé a opakovane použiteľné časti.'
  },
  {
    id: 3,
    title: 'Tretí článok: Budúcnosť webu',
    text: 'Moderné webové aplikácie sú rýchle, interaktívne a optimalizované pre mobilné zariadenia.'
  }
])

const postFontSize = ref(1)
</script>

<template>
 <div class="blog-container">
    <h1>Môj Blog</h1>
    <div :style="{ fontSize: postFontSize + 'em' }">
      <Article 
        v-for="article in articles" 
        :key="article.id"
        :title="article.title" 
        :text="article.text" 
        @enlarge-text="postFontSize += 0.1"
      />
    </div>
  </div>
</template>

<style scoped>
.blog-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}
.blog-container h1 {
  text-align: center;
  color: #42b883;
  margin-bottom: 30px;
}
</style>
