<script setup>
import { onMounted, ref } from 'vue';

const luckyNumber = ref(null);
const text = ref('');
const ulozenyText = ref('');

const text2 = ref('');
const ulozenyText2 = ref('');

function num_gen() {
  return Math.floor(Math.random() * 100) + 1;
}

function ulozText() {
  ulozenyText.value = text.value;
  text.value = '';
}

function ulozText2() {
  ulozenyText2.value = text2.value;
  text2.value = '';
}

function longerthan10() {
  return text.value.length > 10;
}

onMounted(() => {
  luckyNumber.value = num_gen();
});
</script>

<template>
  <h1>My lucky number: {{ luckyNumber }}</h1>

  <textarea
    v-model="text"
    @keydown.enter.prevent="ulozText"
    placeholder="Napíš HTML a stlač Enter..."
  ></textarea>
  <div v-html="ulozenyText"></div>

  <br>
  <br>

  <textarea
    v-model="text2"
    :disabled="jeDlhsiAko10()"
    placeholder="Napíš text..."
  ></textarea>

  <p>Počet znakov: {{ text2.length }}</p>
</template>

<style scoped>
textarea {
  display: block;
  width: 300px;
  height: 100px;
  margin-bottom: 16px;
}
</style>