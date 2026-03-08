<script setup lang="ts">
import type { Product } from "../models/product";

defineProps<{
  product: Product;
}>();

</script>
<template>
  <div class="border border-secondary border-2 rounded-3 p-3">
    <p class="text-start">Nom: {{ product.name }}</p>
    <p class="text-start">Description: {{ product.description }}</p>
    <p class="text-start">Prix: {{ product.price }} $</p>
    <p class="text-start">Stock: {{ product.stock }}</p>
  </div>
</template>
<style scoped></style>
