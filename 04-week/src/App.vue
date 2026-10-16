<script setup>
import { ref } from 'vue'

const items = ref([
  { name: "Ďuso", znamka: 1, poznamka: "" },
  { name: "Peťo", znamka: 2, poznamka: "" },
  { name: "Fero", znamka: 4, poznamka: "" }
])

function pridajElement(name,znamka){
  items.value.push(name,znamka,1)
}

function vymazElement(index){
  items.value.splice(index, 1)
}
</script>

<template>
  <div>
    <ul>
      <li v-for="(item, index) in items" :key="item.name">
        {{ item.name }}
        <input type="text" v-model="item.poznamka">
        <button v-on:click="vymazElement(index)">Vymaž</button>
      </li>
    </ul>

    <br>

    <div class="kontajner">
      <table v-if="items.length > 0">
        <thead>
          <tr>
            <th>Meno študenta</th>
            <th>Známka</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in items" :key="item.name">
            <td>{{ item.name }}</td>
            <td>{{ item.znamka }}</td>
          </tr>
        </tbody>
      </table>
      
      <p v-else class="prazdny-stav">
        Nenašli sa žiadni študenti
      </p>
    </div>
  </div>

  <form>
    <p>Meno</p>
    <input type="text" v-bind="">
    <p>Znamka</p>
    <input type="int" v-model="">
    <button @click="pridajElement(meno,znamka)">Pridaj</button>
  </form>
</template>

<style scoped>
</style>
