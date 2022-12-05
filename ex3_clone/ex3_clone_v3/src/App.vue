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
      <span v-if="onSale">On Sale!</span>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      product: 'Socks',
      image: 'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
      inStock: true,
      onSale:true
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
