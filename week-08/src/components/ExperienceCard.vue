<script setup>
defineProps({
  destinationSlug: { type: String, required: true },
  experience: { type: Object, required: true },
});
</script>

<template>
  <RouterLink
    class="card"
    :to="{
      name: 'experience',
      params: {
        slug: destinationSlug,
        experienceSlug: experience.slug,
      },
    }"
  >
    <img :src="'/images/' + experience.image" :alt="experience.name" />
    <span class="card__text">{{ experience.name }}</span>
  </RouterLink>
</template>
