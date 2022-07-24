<template>
  <component>
    <p>Review form</p>
    <form action="" @submit.prevent="onSubmit" ref="review">
      <h3>Leave a review</h3>
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="rate.name" />

      <label for="review">Review:</label>
      <textarea
        name="review"
        id="review"
        cols="30"
        rows="10"
        v-model="rate.review"
      ></textarea>
      <label for="rating">Rating:</label>
      <select name="rating" id="rating" v-model.number="rate.rating">
        <option value="5">5</option>
        <option value="4">4</option>
        <option value="3">3</option>
        <option value="2">2</option>
        <option value="1">1</option>
      </select>
      <button type="submit">Submit</button>
    </form>
  </component>
</template>

<script setup>
import { ref, toRefs } from "vue";

let component = "review-form";

let rate = ref({
  name: "",
  review: "",
  rating: null,
});

let emit = defineEmits(["review_submitted"]);

const onSubmit = () => {
  let productReview = {
    name: rate.value.name,
    review: rate.value.review,
    rating: rate.value.rating,
  };

  emit("review_submitted", productReview);

  rate.value = {
    name: "",
    review: "",
    rating: null,
  };
};
</script>
