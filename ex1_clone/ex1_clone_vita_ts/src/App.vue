<script setup lang="ts">
import { ref } from "vue";

const product = ref<string>("Socks");
const firstName = ref<string>("KyuSung");
const lastName = ref<string>("Hwang");
const message = ref<string>("This is the sample test message");
const description = ref<string>("A pair of warm, fuzzy socks");
</script>

<template>
  <div id="app">
    <h2>{{ product }}</h2>
    <h2>{{ product + "?" }}</h2>
    <h2>{{ firstName + " " + lastName }}</h2>
    <h2>{{ message.split("").reverse().join("") }}</h2>
    <p>{{ description }}</p>
  </div>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
