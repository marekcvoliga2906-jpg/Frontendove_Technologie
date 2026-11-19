<script setup>
import data from "../data.json";
import { computed } from "vue";

const props = defineProps({
  slug: {
    type: String,
    required: true,
  },
  experienceSlug: {
    type: String,
    required: true,
  },
});

const experience = computed(() => {
  const destination = data.destinations.find(
    (item) => item.slug === props.slug,
  );
  return destination?.experiences.find(
    (item) => item.slug === props.experienceSlug,
  );
});
</script>
<template>
  <article v-if="experience" class="experience-details">
    <h2>{{ experience.name }}</h2>

    <div class="experience-content">
      <img :src="'/images/' + experience.image" :alt="experience.name" />

      <p>{{ experience.description }}</p>
    </div>
  </article>

  <p v-else>Experience not found.</p>
</template>
