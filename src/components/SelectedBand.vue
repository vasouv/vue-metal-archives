<script setup>
import {defineProps, computed, ref, watch} from 'vue';

const props = defineProps({
  bandIndex: {
    type: Number,
    default: 0
  },
  name: {
    type: String,
    default: ''
  },
  spotifyId: {
    type: String,
    default: ''
  }
})

let band = ref({});
let albums = ref([]);
let singles = ref([]);

const spotifyLink = computed(() => {
  return `http://localhost:8080/spotify/band/${props.spotifyId}/albums`;
})

watch(() => [props.bandIndex, props.name, props.spotifyId], () => {
  fetchAlbums()
})

async function fetchAlbums() {
  try {
    const response = await fetch(spotifyLink.value);
    const data = await response.json();
    singles.value = data.filter(a => a.type === 'SINGLE')
    albums.value = data.filter(a => a.type === 'ALBUM')
  } catch (e) {
    console.error('Error fetching albums', e);
  }
}

</script>

<template>
  <h2>{{ name }} Albums</h2>
  Spotify ID: {{ spotifyId }}
  <h3>Albums</h3>
  {{  albums }}
  <h3>Singles</h3>
  {{ singles }}

</template>

<style scoped>

</style>