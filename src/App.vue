<script setup>
  import { ref } from "vue";
  const selectedBand = ref('');

  const bands = [
    {id: 184, name: 'Bathory'},
    {id: 4, name: 'Iced Earth'},
    {id: 150, name: 'Amon Amarth'}
  ]
</script>

<template>
  <header class="container">
    <h1>Vue Metal Archives API</h1>
  </header>

  <main class="container">
    <label for="band-select">Select Band:</label>
    <select id="band-select" v-model="selectedBand">
      <option value="" disabled>- Select Band -</option>
      <option value="184">Bathory</option>
      <option value="4">Iced Earth</option>
      <option value="150">Amon Amarth</option>
    </select>

    <span>Selected band ID is: {{ selectedBand }}</span>

  </main>
</template>
