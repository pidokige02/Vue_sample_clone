<template>
  <div class="nav-bar"></div>
  <div class="cart">
    <p>Cart({{ cart.length }})</p>
  </div>
  <product :premium="premium" @add-to-cart="updateCart"  @remove-from-cart="removeItem"></product>
</template>

<script>
import Product from '@/components/Product'

export default {
  name: 'App',
  components: {
    Product
  },
  data() {
    return{
      premium : true,
      cart : []
    }
  },
  methods: {
      updateCart(id) {
        this.cart.push(id)
      },
      removeItem(id) {
        for(var i = this.cart.length - 1; i >= 0; i--) {
          if (this.cart[i] === id) {
             this.cart.splice(i, 1);
             break;
          }
        }
      }
  }
}
</script>

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
