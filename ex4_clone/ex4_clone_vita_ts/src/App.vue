<script setup lang="ts">
import {ref} from "vue";
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
const variants = ref<
  {
    variantId: number;
    variantColor: string;
  }[]
>([
  {
    variantId: 2234,
    variantColor: "green",
  },
  {
    variantId: 2235,
    variantColor: "blue",
  },
]);
const sizes = ref<string[]>(["S", "M", "L", "XL", "XXL", "XXXL"]);
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
        <p>{{ variant.variantColor }}</p>
      </div>

      <ul>
        <li v-for="size in sizes" :key="size.id">{{ size }}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
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
