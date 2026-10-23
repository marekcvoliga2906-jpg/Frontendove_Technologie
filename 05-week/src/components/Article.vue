<script setup>
defineProps({
  title: {
    type: String,
  },
  text: {
    type: String,
  }
})

const emit = defineEmits(['enlarge-text'])
</script>

<template>
  <article class="article-card">
    <h2>{{ title }}</h2>
    <p>{{ text }}</p>
    <button @click="emit('enlarge-text')">Zväčšiť text</button>
  </article>
</template>

<style scoped>
.article-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 16px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}
.article-card h2 {
  margin-top: 0;
  color: #2c3e50;
}
</style>
