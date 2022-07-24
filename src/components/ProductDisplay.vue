/*html*/
<template>
  <compose>
    <div class="product-display">
      <div class="product-container">
        <div class="product-image">
          <img
            :src="image"
            alt="socks"
            :class="inStock < 1 && 'out-of-stock-img'"
          />
        </div>
        <div class="product-info">
          <h1>{{ product }}</h1>
          <p>{{ inStock }}</p>
          <p v-if="inStock > 10">In Stock</p>
          <p v-else-if="inStock <= 10 && inStock > 0">Running out</p>
          <p v-else>Out of Stock</p>
          <div v-for="variant in variants" :id="variant.id">
            {{ variant.color }}
          </div>
          <div v-for="size in sizes" :key="size.id">
            {{ size.size }}
          </div>
          <div
            v-for="(variant, index) in variants"
            :key="variant.id"
            class="color-circle"
            :style="{ backgroundColor: variant.color }"
            @mouseover="updateVariant(index)"
          >
            <!-- {{ variant.color }} -->
          </div>
          <button
            class="button"
            :disabled="inStock < 1"
            @click="addToCart"
            :class="{ disabledButton: inStock < 1 }"
          >
            Add to cart
          </button>
        </div>
      </div>
    </div>
    <ReviewList v-if="reviews.length" :reviews="reviews" />
    <Form @review_submitted="addReview"></Form>
  </compose>
</template>

<script setup>
import { computed, ref, defineEmits } from "vue";
import Form from "./Form.vue";
import ReviewList from "./ReviewList.vue";
let compose = "product-display";
let product = "Sucks";
let image = ref("./src/assets/socks_green.jpg");
let selectedVariant = 0;

let variants = ref([
  {
    id: 221,
    color: "blue",
    image: "./src/assets/socks_blue.jpg",
    quantity: 11,
  },
  {
    id: 222,
    color: "green",
    image: "./src/assets/socks_green.jpg",
    quantity: 2,
  },
]);
let sizes = [
  { id: 331, size: "small" },
  { id: 332, size: "medium" },
  { id: 333, size: "large" },
  { id: 334, size: "extra-large" },
];

let reviews = ref([]);
let inStock = ref(variants.value[selectedVariant].quantity);

const addToCart = () => {
  if (!variants.value[selectedVariant].quantity < 1) {
    console.log("clicked");
    variants.value[selectedVariant].quantity--;
    inStock.value = variants.value[selectedVariant].quantity;
    emit("add-to-cart", variants.value[selectedVariant].id);
  }
};
let isActive = true;

// const updateVariant = computed((index) => {
//   selectedVariant = index;
//   console.log(index);
// });

const emit = defineEmits(["add-to-cart", "add-to-cart:id"]);

const updateVariant = (index) => {
  selectedVariant = index;
  image.value = variants.value[selectedVariant].image;
  inStock.value = variants.value[selectedVariant].quantity;
  console.log(inStock.value);
};

const addReview = (review) => {
  reviews.value.push(review);
  console.log(reviews.value.length);
};
</script>
