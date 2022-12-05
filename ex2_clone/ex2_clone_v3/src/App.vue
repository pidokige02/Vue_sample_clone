<template>
  <div class="product">

    <div class="product-image">
      <img v-bind:src="image" v-bind:alt="altText" /> <!-- scr, alt are the attributes we are binding data to -->
      <a v-bind:href="link" target="_blank">More products like this</a>
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  setup() {
    return {
      product : 'Socks',
      image : 'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
      altText : "socks images",
      link : 'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
    }
  }
}
</script>

<style>
body {
    font-family: tahoma;
    color:#282828;
    margin: 0px;
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
