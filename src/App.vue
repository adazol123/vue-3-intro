<script setup>
import { ref } from "vue";
import ProductDisplay from "./components/ProductDisplay.vue";
import Form from "./components/Form.vue";
let cart = ref([]);

/** `updateCart` function --- Accepts {ID} payload from emit in product_display component */
const updateCart = (id) => {
  cart.value.push(id);
};
</script>

<template>
  <main>
    <div class="nav-bar"></div>
    <div class="cart">Cart({{ cart.length }})</div>
    <ProductDisplay @add-to-cart="updateCart" />
  </main>
</template>
