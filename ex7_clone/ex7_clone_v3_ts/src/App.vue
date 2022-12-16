<template>
  <div class="nav-bar"></div>

  <div class="product">
    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <!-- title is a computed  property -->
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>
      <p>{{ sale }}</p>

      <ul>
        <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
      </ul>

      <div
        class="color-box"
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>

      <button
        v-on:click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >
        Add to cart
      </button>
      <button
        @click="removeFromCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >
        Remove from cart
      </button>

      <div class="cart">
        <p>Cart({{ cart }})</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from "vue";

export default defineComponent({
  name: "App",
  setup() {
    const product = ref("Socks");
    const brand = ref("Vue Mastery");
    const selectedVariant = ref(0);
    const details = ref(["80% cotton", "20% polyester", "Gender-neutral"]);

    const variants = ref([
      {
        variantId: 2234,
        variantColor: "green",
        variantImage:
          "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
        variantQuantity: 10,
      },
      {
        variantId: 2235,
        variantColor: "blue",
        variantImage:
          "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg",
        variantQuantity: 0,
      },
    ]);

    const cart = ref(0);
    const onSale = ref(true);

    const addToCart = () => {
      cart.value += 1;
    };

    const updateProduct = (index: number) => {
      selectedVariant.value = index;
    };

    const removeFromCart = () => {
      if (cart.value > 0) cart.value -= 1;
    };

    const title = computed(() => {
      return brand.value + " " + product.value;
    });

    const image = computed(() => {
      return variants.value[selectedVariant.value].variantImage;
    });

    const inStock = computed(() => {
      return variants.value[selectedVariant.value].variantQuantity;
    });

    const sale = computed(() => {
      if (onSale.value) {
        return brand.value + " " + product.value + " are on sale!";
      }
      return brand.value + " " + product.value + " are not on sale";
    });

    return {
      product,
      brand,
      selectedVariant,
      details,
      variants,
      cart,
      onSale,
      addToCart,
      updateProduct,
      removeFromCart,
      title,
      image,
      inStock,
      sale,
    };
  },
});
</script>

<style>
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

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
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
