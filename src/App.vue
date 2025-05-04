<script setup lang="ts">
import { ref } from "vue";
import Card from "./components/Card.vue";

const input = ref("");
const countries = ref();

async function fetchCountries() {
  const response = await fetch(`https://restcountries.com/v3.1/name/${input.value}`);
  const data = await response.json();
  countries.value = data;
}
</script>

<template>
  <h1>Country Info</h1>

  <form @submit.prevent="fetchCountries">
    <input v-model="input" placeholder="country name" />
    <button type="submit">Fetch</button>
  </form>

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
h1{
  height: 1em;
  padding: 1em;
  will-change: filter;
  transition: filter 300ms;
  filter: drop-shadow(0 0 2em rgb(183, 242, 124));
}
button:hover {
  filter: drop-shadow(0 0 2em #95fd17aa);
}
article:hover {
  filter: drop-shadow(0 0 2em #f69f12aa);
}
</style>
