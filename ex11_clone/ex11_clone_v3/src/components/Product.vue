<template>
   <div class="product">

        <div class="product-image">
          <img :src="image" />
        </div>

        <div class="product-info">
            <h1>{{  title  }}</h1>
            <p v-if="inStock">In Stock</p>
            <p v-else>Out of Stock</p>
            <p>Shipping: {{ shipping }}</p>

            <product-details :details="details"></product-details>

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

        </div>

    </div>

    <product-tabs :reviews="reviews"></product-tabs>

</template>


<script>
import ProductDetails from '@/components/ProductDetails'
import ProductTabs from '@/components/ProductTabs'

export default {
    name: 'product',
    components: {
        ProductDetails,
        ProductTabs
    },
    props: {
        premium: {
            type: Boolean,
            required: true
       }
    },
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
            reviews: []
        }
  },
  methods: {
      addToCart: function() {
        this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
      },
      updateProduct: function(index) {
          this.selectedVariant = index
      },
      removeFromCart : function() {
        this.$emit('remove-from-cart', this.variants[this.selectedVariant].variantId)
      },
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
      shipping() {
          if (this.premium) {
            return "Free"
          }
          else  return 2.99
      }
   },
   mounted() {
        this.emitter.on('review-submitted', productReview => {
          this.reviews.push(productReview)
        })
    }
}

</script>

<style scoped>
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

.color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
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