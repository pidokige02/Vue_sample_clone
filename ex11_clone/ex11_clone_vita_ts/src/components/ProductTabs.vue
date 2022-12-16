<script setup lang="ts">
import { ref } from "vue";
import ProductReview from "@/components/ProductReview.vue";

defineProps({
  reviews: {
    type: Array,
    required: false,
  },
});

const tabs = ref(["Reviews", "Make a Review"]);
const selectedTab = ref("Reviews"); // set from @click
</script>

<template>
  <div>
    <div>
      <span
        class="tabs"
        :class="{ activeTab: selectedTab === tab }"
        v-for="(tab, index) in tabs"
        :key="index"
        @click="selectedTab = tab"
        >{{ tab }}</span
      >
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

<style scoped>
.tabs {
  margin-left: 20px;
  cursor: pointer;
}

.activeTab {
  color: #16c0b0;
  text-decoration: underline;
}
</style>
