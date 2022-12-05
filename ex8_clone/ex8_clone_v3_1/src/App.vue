<template>
  <div class="nav-bar"></div>
  <product :premium="premium"></product>
</template>

<script>
import { ref } from 'vue'
import Product from '@/components/Product'

export default {
  name: 'App',
  components: {
    Product
  },
  setup () {
    const premium = ref(true)
    return {
      premium
    }
  }
  // data() {
  //   return{
  //     premium : false
  //   }
  // }
}
</script>

<style scoped>
.nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
}

</style>
