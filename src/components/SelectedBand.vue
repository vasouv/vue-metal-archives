<script setup>
import {defineProps} from 'vue';

defineProps({
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

</script>

<template>
  <h2>{{ name }} Albums</h2>
  Metal Archives ID: {{ metalArchivesId }}
</template>

<style scoped>

</style>