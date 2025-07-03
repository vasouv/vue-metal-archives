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

  <article>
    <header>{{ year }} - {{ title }}</header>
    {{ imageUrl }}
<!--    <img :src="imageUrl" height="160" width="160" />-->
  </article>

</template>

<style scoped>

</style>