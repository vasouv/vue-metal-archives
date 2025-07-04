<script setup>
import {computed, ref, watch} from 'vue';
import Album from "@/components/Album.vue";

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
  if (props.spotifyId === '') {
    alert("Spotify link was not found.");
    return;
  }
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
  <h2>{{ name }}</h2>

  <h3>Albums</h3>
  <section class="container-fluid">
    <div class="album-grid">
      <Album v-for="(album, index) in albums" :key="index" :releaseDate="album.releaseDate" :title="album.title" :imgLink="album.imageUrl"/>
    </div>
  </section>

  <h3>Singles</h3>
  <section class="container-fluid">
    <div class="album-grid">
      <Album v-for="(single, index) in singles" :key="index" :releaseDate="single.releaseDate" :title="single.title" :imgLink="single.imageUrl"/>
    </div>
  </section>

</template>

<style scoped>
h2 {
  text-align: center;
}
.album-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}
</style>