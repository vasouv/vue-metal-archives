<script setup>
import {ref} from "vue";
import {BANDS} from "./bands.js";
import SelectedBand from "@/components/SelectedBand.vue";

const bandIndex = ref(0);
const name = ref("");
const spotifyId = ref(0);

const bands = BANDS.toSorted((a, b) => a.name.localeCompare(b.name));

const selectBand = (index) => {
  bandIndex.value = index;
  name.value = bands[index].name;
  spotifyId.value = bands[index].spotify_link;
}

</script>

<template>

  <header class="container-fluid">
    <h1>Metal Vuer</h1>
  </header>

  <main class="container-fluid">

    <div id="metal-grid" class="grid-layout">

      <!-- bands list -->
      <aside id="bands-list" class="band-sidebar">
        <ul>
          <li v-for="(band, index) in bands" :key="band.name" @click="selectBand(index)">
            <a role="button" :class="{ active: bandIndex === index }">{{ band.name }}</a>
          </li>
        </ul>
      </aside>

      <!-- selected band -->
      <section id="band-selection">
        <SelectedBand :bandIndex="bandIndex" :name="name" :spotifyId="spotifyId" />
      </section>

    </div>

  </main>

</template>

<style scoped>

/* Main layout */
.grid-layout {
  display: flex;
  gap: 2rem;
  align-items: flex-start;
  flex-wrap: wrap; /* allows stacking on small screens */
}

/* Sidebar */
.band-sidebar {
  display: inline-block;
  padding: 1rem;
  background-color: var(--pico-background);
  border-radius: 0.5rem;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.05);
  white-space: nowrap; /* Prevent text wrapping */
}

.band-sidebar ul {
  display: flex;
  flex-direction: column;
  align-items: stretch; /* makes all children (li) the same width */
}

.band-sidebar li {
  width: 100%; /* ensure all buttons take the full width of the sidebar */
}

.band-sidebar a[role="button"] {
  display: block;
  width: 100%;
  text-align: left;
  padding: 0.5rem 1rem;
  border-radius: 0.25rem;
  cursor: pointer;
  transition: background-color 0.2s ease;
  box-sizing: border-box;
}

.band-sidebar a[role="button"]:hover {
  background-color: var(--pico-muted-color);
}

.band-sidebar a.active {
  background-color: var(--pico-primary);
  color: var(--pico-primary-inverse);
}

/* Selected band section takes the rest of the space */
#band-selection {
  flex: 1;
  min-width: 0; /* prevents overflow issues */
}

</style>
