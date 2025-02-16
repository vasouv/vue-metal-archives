<script setup>
import {defineProps, computed, ref} from 'vue';

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
    default: 0
  }
})

let band = ref({});

const metalArchivesLink = computed(() => {
  if (props.metalArchivesId === 0) {
    band = {};
  } else {
    band = {name: "Test band"};
  }
  // return 'https://metal-api.dev/bands/' + props.metalArchivesId;
})

</script>

<template>
  <h2>{{ name }} Albums</h2>
  Metal Archives ID: {{ metalArchivesId }}
  <br>
  Metal Archives Band: {{ metalArchivesLink }}
  <br>
  {{ band }}

</template>

<style scoped>

</style>