<template>
  <ul>
    <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
  </ul>
</template>

<script lang="ts">
export default {
  name: "product-details",
  props: {
    details: {
      type: Array,
      required: true,
    },
  },
};
</script>
