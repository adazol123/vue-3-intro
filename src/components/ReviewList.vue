<template>
  <compoment>
    <h3>Review:</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        <p>{{ review.name }} game this {{ review.rating }} stars</p>
        <br />
        <p>{{ review.review }}</p>
      </li>
    </ul>
  </compoment>
</template>

<script setup>
import { onMounted, ref } from "vue";

let compoment = "review-list";
const props = defineProps({
  reviews: {
    type: Array,
  },
});
let reviews = props.reviews;
</script>
