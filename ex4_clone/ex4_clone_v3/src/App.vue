<template>
  <div class="nav-bar"></div>

  <div class="product">

    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>

      <ul>
        <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
      </ul>

      <div v-for="variant in variants" :key="variant.variantId">
        <p>{{ variant.variantColor }}</p>
      </div>

      <ul>
        <li v-for="size in sizes" :key="size.id">{{ size }}</li>
      </ul>

    </div>

</div>

</template>
<script>
import { ref } from "vue"

export default {
  name: 'App',
  setup () {
    const product = ref('Socks')
    const image = ref('https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg')
    const inStock = ref(true)
    const details = ref(['80% cotton', '20% polyester', 'Gender-neutral'])
    const variants = ref(
       [
        {
          variantId: 2234,
          variantColor: 'green'
        },
        {
          variantId: 2235,
          variantColor: 'blue'
        }
      ])

    const sizes = ref( ['S', 'M', 'L', 'XL', 'XXL', 'XXXL'])
    return {
      product,
      image,
      inStock,
      details,
      variants,
      sizes
    }
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

body {
    font-family: tahoma;
    color:#282828;
    margin: 0px;
}

.nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
}

.product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
}

img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
}

.product-image {
    width: 80%;
}

.product-image,
.product-info {
    margin-top: 10px;
    width: 50%;
}


</style>
