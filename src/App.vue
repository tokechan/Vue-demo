<script setup lang="ts">
import { ref } from "vue";
import Card from "./components/Card.vue";


const countries = ref();

async function fetchCountries() {
  const response = await fetch("https://restcountries.com/v3.1/name/japan");
  const data = await response.json();
  countries.value = data;
}
</script>

<template>
  <h1>Country Info</h1>

  <button type="button" @click="fetchCountries">Fetch</button>

  <Card
   v-for="country in countries"
    :key="country.name.common"
    :name="country.name.common"
    :image="country.flags.png"
    :tldList="country.tld"
    :currencies="country.currencies"
  />

  <!-- <div>{{ countries }}</div> -->
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
button:hover {
  filter: drop-shadow(0 0 2em #95fd17aa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #f69f12aa);
}
</style>
