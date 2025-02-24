<script setup>
import {defineProps, computed, ref, onUpdated, onMounted} from 'vue';

const props = defineProps({
  bandIndex: {
    type: Number,
    default: 0
  },
  name: {
    type: String,
    default: ''
  },
  metalArchivesId: {
    type: Number,
    default: 89238
  }
})

let band = ref({});
let albums = ref([]);

const metalArchivesLink = computed(() => {
  return `http://localhost:8080/metalapi/band/${props.metalArchivesId}/albums`;
})

onMounted(async () => {
  const albumsLink = `http://localhost:8080/metalapi/band/${props.metalArchivesId}/albums`;
  try {
    const response = await fetch(albumsLink);
    const data = await response.json();
    console.log(data);
    albums.value = data;
    // albums.value = data.map(bandResponse => bandResponse.albums);
  } catch (e) {
    console.error('Error fetching albums', e);
  }
})

</script>

<template>
  <h2>{{ name }} Albums</h2>
  Metal Archives ID: {{ metalArchivesId }}
  <br>
  Metal Archives Band: {{ metalArchivesLink }}
  <br>
  {{ albums }}

</template>

<style scoped>

</style>