<script setup>
import {computed} from "vue";

const props = defineProps({
  releaseDate: {
    type: String,
    default: ''
  },
  title: {
    type: String,
    default: ''
  },
  imgLink: {
    type: String,
    default: ''
  }
})

const year = computed(() => {
  if (props.releaseDate === '') return '';
  return `${props.releaseDate}`.substring(0,4)
})

const imageUrl = computed(() => {
  if (props.imgLink === '') return '';
  return new URL(props.imgLink, import.meta.url).href;
})

</script>

<template>

  <article class="album-card">
    <header>{{ year }} - {{ title }}</header>
    <img :src="imageUrl" height="160" width="160" />
  </article>

</template>

<style scoped>
.album-card {
  padding: 1rem;
  border-radius: 0.5rem;
  background-color: var(--pico-background);
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.05);
  text-align: center;
  transition: transform 0.2s ease;
}

.album-card:hover {
  transform: translateY(-4px);
}

.album-card img {
  max-width: 100%;
  border-radius: 0.5rem;
  margin-bottom: 0.75rem;
}
</style>