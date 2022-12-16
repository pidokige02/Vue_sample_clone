<script setup lang="ts">
import { ref } from "vue";
import Product from "./components/Product.vue";

const premium = ref(true);
</script>

<template>
  <div class="nav-bar"></div>
  <product :premium="premium"></product>
</template>

<style scoped>
.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}
</style>
