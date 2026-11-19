<script setup>
import data from "../data.json";
import { computed } from "vue";
const destinations = data.destinations;
</script>

<template>
  <section class="home">
    <h1>All destinations</h1>

    <div class="destinations">
      <div v-for="destination in destinations" :key="destination.id">
        <RouterLink
          :to="{ name: 'destination', params: { slug: destination.slug } }"
        >
          <h2>
            {{ destination.name }}
          </h2>

          <img :src="'/images/' + destination.image" :alt="destination.name" />
        </RouterLink>
      </div>
    </div>
  </section>
</template>
