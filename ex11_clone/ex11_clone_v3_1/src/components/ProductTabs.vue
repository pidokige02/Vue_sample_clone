<template>
    <div>

      <div>
        <span class="tabs"
              :class="{ activeTab: selectedTab === tab }"
              v-for="(tab, index) in tabs"
              :key="index"
              @click="selectedTab = tab"
        >{{ tab }}</span>
      </div>

      <div v-show="selectedTab === 'Reviews'">
          <p v-if="!reviews.length">There are no reviews yet.</p>
          <ul v-else>
              <li v-for="review in reviews" :key="review.id">
                <p>{{ review.name }}</p>
                <p>Rating:{{ review.rating }}</p>
                <p>{{ review.review }}</p>
              </li>
          </ul>
      </div>

      <div v-show="selectedTab === 'Make a Review'">
        <product-review></product-review>
      </div>

    </div>

</template>


<script>
import { ref } from 'vue'
import ProductReview from '@/components/ProductReview'

export default {
    name: 'product-tabs',
    components: {
        ProductReview,
    },
    props: {
      reviews: {
        type: Array,
        required: false
      }
    },
    setup() {
        const tabs = ref(['Reviews', 'Make a Review'])
        const selectedTab = ref('Reviews')  // set from @click

        return {
            tabs,
            selectedTab
        }
    }
}
</script>

<style scoped>
.tabs {
    margin-left: 20px;
    cursor: pointer;
}

.activeTab {
    color: #16C0B0;
    text-decoration: underline;
}

</style>