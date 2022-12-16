<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <div class="error" v-if="errors.length">
      <div>
        <b>Please correct the following error(s):</b>
        <ul>
          <li v-for="error in errors" :key="error.id">{{ error }}</li>
        </ul>
      </div>
    </div>

    <p>
      <label for="name">Name:</label>
      <input id="name" v-model="name" />
    </p>

    <p>
      <label for="review">Review:</label>
      <textarea id="review" v-model="review"></textarea>
    </p>

    <p>
      <label for="rating">Rating:</label>
      <select id="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
    </p>

    <p>Would you recommend this product?</p>
    <label>
      Yes
      <input type="radio" value="Yes" v-model="recommend" />
    </label>
    <label>
      No
      <input type="radio" value="No" v-model="recommend" />
    </label>

    <p>
      <input type="submit" value="Submit" />
    </p>
  </form>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "product-review",

  setup(props, { emit }) {
    const name = ref<string>("");
    const review = ref<string>("");
    const rating = ref<string>("");
    const recommend = ref<string>("");
    const errors = ref<string[]>([]);

    const onSubmit = () => {
      errors.value = [];
      if (name.value && review.value && rating.value && recommend.value) {
        let productReview = {
          name: name.value,
          review: review.value,
          rating: rating.value,
          recommend: recommend.value,
        };
        emit("review-submitted", productReview);
        // send up data from our child to our parent when an event occurs.
        // event name is 'review-submitted'.
        name.value = "";
        review.value = "";
        rating.value = "";
        recommend.value = "";
      } else {
        if (!name.value) errors.value.push("Name required.");
        if (!review.value) errors.value.push("Review required.");
        if (!rating.value) errors.value.push("Rating required.");
        if (!recommend.value) errors.value.push("Recommendation required.");
      }
    };
    return {
      name,
      review,
      rating,
      recommend,
      errors,
      onSubmit,
    };
  },
});
</script>

<style scoped>
.review-form {
  width: 400px;
  padding: 20px;
  margin: 40px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}

.tab {
  margin-left: 20px;
  cursor: pointer;
}

.activeTab {
  color: #16c0b0;
  text-decoration: underline;
}
</style>
