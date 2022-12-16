<script setup>
import { ref } from 'vue'
import Product from './components/Product.vue'

const premium = ref(false)
</script>

<template>
  <div class="nav-bar"></div>
  <product :premium="premium"></product>
</template>

<style scoped>
.nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
}
</style>
