<template>
  <div class="nav-bar"></div>

  <div class="product">

      <div class="product-image">
          <img :src="image" />
      </div>

      <div class="product-info">
          <h1>{{ title }}</h1>  <!-- title is a computed  property -->
          <p v-if="inStock">In Stock</p>
          <p v-else>Out of Stock</p>
          <p>{{ sale }}</p>

          <ul>
            <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
          </ul>


          <div class="color-box"
             v-for="(variant, index) in variants"
                 :key="variant.variantId"
                 :style="{ backgroundColor: variant.variantColor }"
                 @mouseover="updateProduct(index)"
                 >
          </div>

          <button v-on:click="addToCart"
              :disabled="!inStock"
              :class="{ disabledButton: !inStock }"
              >
            Add to cart
          </button>
          <button @click="removeFromCart"
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

<script>

export default {
  name: 'App',
  data() {
    return {
      product: 'Socks',
      brand: 'Vue Mastery',
      selectedVariant: 0,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage:  'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
          variantQuantity: 10
        },
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: 'https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg',
          variantQuantity: 0
        }
      ],
      cart: 0,
      onSale: true
    }
  },
  methods: {
      addToCart: function() {
          this.cart += 1
      },
      updateProduct: function(index) {
          this.selectedVariant = index
      },
      removeFromCart() {
          if(this.cart > 0)
            this.cart -= 1
      }
  },
  computed: {
      title() {
          return this.brand + ' ' + this.product
      },
      image(){
          return this.variants[this.selectedVariant].variantImage
      },
      inStock(){
          return this.variants[this.selectedVariant].variantQuantity
      },
      sale() {
        if (this.onSale) {
          return this.brand + ' ' + this.product + ' are on sale!'
        }
          return  this.brand + ' ' + this.product + ' are not on sale'
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
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
}

.disabledButton {
    background-color: #d8d8d8;
}

</style>
