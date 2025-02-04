<script setup>
import {ref} from "vue";
import {BANDS} from "./bands.js";

const selectedBand = ref('');

const bands = BANDS.toSorted((a, b) => a.name.localeCompare(b.name));

const selectBand = (index) => {
  selectedBand.value = bands[index].name;
}

</script>

<template>

  <header class="container">
    <h1>Metal Vuer</h1>
  </header>

  <main class="container">

    <div id="metal-grid" class="grid">

      <!-- bands list -->
      <aside id="bands-list">
        <ul>
          <li v-for="(band, index) in bands" :key="band">
            <span @click="selectBand(index)">{{ band.name }}</span>
          </li>
        </ul>
      </aside>

      <!-- selected band -->
      <section id="band-selection">
        <h2>{{ selectedBand }}</h2>
      </section>

    </div>

  </main>

</template>

<style scoped>

#metal-grid {
  display: grid;
  grid-template-columns: 1fr 4fr;
  grid-template-rows: 1fr;
  grid-column-gap: 0px;
  grid-row-gap: 0px;
}

#bands-list {
  background-color: gainsboro;
}

#band-selection {
  background-color: khaki;
}

</style>
