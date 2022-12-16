<template>
  <div class="nav-bar"></div>
  <product :premium="premium"></product>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Product from "@/components/Product.vue";

export default defineComponent({
  name: "App",
  components: {
    Product,
  },
  setup() {
    const premium = ref(true);
    return {
      premium,
    };
  },
  // data() {
  //   return{
  //     premium : false
  //   }
  // }
});
</script>

<style>
.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}
</style>
