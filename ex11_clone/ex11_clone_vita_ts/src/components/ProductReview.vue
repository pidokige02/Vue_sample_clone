<script setup lang="ts">
import { ref, getCurrentInstance } from "vue";

const internalInstance = getCurrentInstance();
const emitter = internalInstance?.appContext.config.globalProperties.emitter;

const name = ref<string>("");
const review = ref<string>("");
const rating = ref<string>("");
const errors = ref<string[]>([]);

const onSubmit = () => {
  errors.value = [];
  if (name.value && review.value && rating.value) {
    let productReview = {
      name: name.value,
      review: review.value,
      rating: rating.value,
    };

    emitter.emit("review-submitted", productReview);

    name.value = "";
    review.value = "";
    rating.value = "";
  } else {
    if (!name.value) errors.value.push("Name required.");
    if (!review.value) errors.value.push("Review required.");
    if (!rating.value) errors.value.push("Rating required.");
  }
};
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <p>
      <label for="name">Name:</label>
      <input class="name" v-model="name" />
    </p>

    <p>
      <label for="review">Review:</label>
      <textarea class="review" v-model="review"></textarea>
    </p>

    <p>
      <label for="rating">Rating:</label>
      <select class="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
    </p>

    <p>
      <input type="submit" value="Submit" />
    </p>
  </form>
</template>

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
