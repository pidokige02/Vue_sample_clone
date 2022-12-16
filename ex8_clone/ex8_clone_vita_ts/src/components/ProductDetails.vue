<script setup lang="ts">
defineProps({
  details: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <ul>
    <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
  </ul>
</template>
