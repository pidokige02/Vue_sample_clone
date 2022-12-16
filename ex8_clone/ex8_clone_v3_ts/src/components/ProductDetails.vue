<template>
  <ul>
    <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
  </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "product-details",
  props: {
    details: {
      type: Array,
      required: true,
    },
  },
});
</script>
