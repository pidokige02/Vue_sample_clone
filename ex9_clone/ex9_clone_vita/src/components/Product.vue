<script setup>
import { ref, computed } from 'vue'
import ProductDetails from '@/components/ProductDetails.vue'

const {premium}  = defineProps({
    premium: {
        type: Boolean,
        required: true
    }
})

const emit = defineEmits(['add-to-cart','remove-from-cart'])

const product = ref('Socks')
const brand = ref('Vue Mastery')
const selectedVariant = ref(0)
const details = ref(['80% cotton', '20% polyester', 'Gender-neutral'])

const variants = ref([
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
])

const addToCart = () => {
    emit('add-to-cart', variants.value[selectedVariant.value].variantId)
}

const updateProduct = (index) => {
  selectedVariant.value = index
}
const removeFromCart = () => {
    emit('remove-from-cart', variants.value[selectedVariant.value].variantId)
}

const title = computed(() => {
      return brand.value + ' ' + product.value
})

const image = computed(() => {
      return variants.value[selectedVariant.value].variantImage
})

const inStock = computed(() => {
      return variants.value[selectedVariant.value].variantQuantity
})

const shipping = computed(() => {
    if (premium) {
        return "Free"
    } else
        return 2.99
})

</script>

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
</template>

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