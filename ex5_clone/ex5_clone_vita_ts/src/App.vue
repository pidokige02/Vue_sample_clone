<script setup lang="ts">
import { ref } from "vue";

interface Variant {
  variantId: number;
  variantColor: string;
  variantImage: string;
}

const product = ref<string>("Socks");
const image = ref<string>(
  "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg"
);
const inStock = ref<boolean>(true);
const details = ref<string[]>([
  "80% cotton",
  "20% polyester",
  "Gender-neutral",
]);

const variants = ref<Variant[]>([
  {
    variantId: 2234,
    variantColor: "green",
    variantImage:
      "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
  },
  {
    variantId: 2235,
    variantColor: "blue",
    variantImage:
      "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg",
  },
]);

const cart = ref<number>(0);

const addToCart = () => (cart.value += 1);
const updateProduct = (variantImage: string) => {
  image.value = variantImage;
};
const removeFromCart = () => {
  if (cart.value > 0) cart.value -= 1;
};
</script>

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
        <p @mouseover="updateProduct(variant.variantImage)">
          {{ variant.variantColor }}
        </p>
      </div>

      <button v-on:click="addToCart">Add to cart</button>
      <button @click="removeFromCart">Remove from cart</button>

      <div class="cart">
        <p>Cart({{ cart }})</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
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
  box-shadow: 0px 0.5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  margin-top: 10px;
  width: 50%;
}

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
}

.disabledButton {
  background-color: #d8d8d8;
}
</style>
