<script setup>

import { ref,computed } from 'vue'

const count = ref(0)

const headingClass = computed(() => {
  return {
    zelena: count.value > 0,
    cervena: count.value < 0,
    siva: count.value == 0
  };
});

const squared = computed(() => {
  return count.value * count.value
})


function increment() {
  if (count.value < 5) {
    count.value++;
  }
  else{
    hidden
  }
}

function decrement() {
  if (count.value>5){
count.value--
  }
else{
    hidden
  }
}

function reset() {
  count.value = 0
}

</script>
<template>
  <header> 
  </header>

  <h2 :class="headingClass">
  Current count: {{ count }}
  </h2>
  <br>
  <p>Druhá mocnina: {{ squared }}</p>
  <br>
  <div class="button-group">
  <button @click="increment">increment</button>
  <button @click="decrement">decrement</button>
  <button @click="reset">reset</button>
  </div>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
  .cervena { background-color: red; }
  .zelena  { background-color: green; }
  .siva    { background-color: gray; }

  .button-group {
  display: flex;
}

.hidden { display: none; } 

}
</style>
