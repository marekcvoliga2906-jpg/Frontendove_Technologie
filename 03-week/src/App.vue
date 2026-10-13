<script setup>
import { onMounted, ref } from 'vue';

const luckyNumber = ref(null);
const text = ref('');
const ulozenyText = ref('');

const text2 = ref('');
const ulozenyText2 = ref('');
const columns = ref(30);
const rows = ref(5);

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

function jeDlhsiAko10() {
  return text2.value.length > 10;
}

function vymazText2() {
  text2.value = '';
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

  <label>
    Počet stĺpcov:
    <input v-model.number="columns" type="number" min="1">
  </label>
  <label>
    Počet riadkov:
    <input v-model.number="rows" type="number" min="1">
  </label>

  <textarea
    v-model="text2"
    :cols="columns"
    :rows="rows"
    :disabled="jeDlhsiAko10()"
    class="dimensioned-textarea"
    placeholder="Napíš text..."
  ></textarea>

  <p>Počet znakov: {{ text2.length }}</p>
  <button v-if="jeDlhsiAko10()" type="button" @click="vymazText2">
    Vyprázdniť reťazec
  </button>
</template>

<style scoped>
textarea {
  display: block;
  width: 300px;
  height: 100px;
  margin-bottom: 16px;
}

.dimensioned-textarea {
  width: auto;
  height: auto;
}

label {
  display: inline-block;
  margin: 0 16px 16px 0;
}

input {
  width: 64px;
  margin-left: 6px;
}
</style>