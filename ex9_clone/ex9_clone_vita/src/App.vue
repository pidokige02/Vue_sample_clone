<script setup>
import { ref } from 'vue'
import Product from '@/components/Product.vue'

const premium = ref(false)
const cart = ref([])

const updateCart = (id) => {
    cart.value.push(id)
}

const  removeItem = (id) => {
  for(var i = cart.value.length - 1; i >= 0; i--) {
      if (cart.value[i] === id) {
          cart.value.splice(i, 1);
             break;
      }
  }
}

</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">
    <p>Cart({{ cart.length }})</p>
  </div>
  <product :premium="premium" @add-to-cart="updateCart"  @remove-from-cart="removeItem"></product>
</template>

<style scoped>
.nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
}
.cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
}
</style>
