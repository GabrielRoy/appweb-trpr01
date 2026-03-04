<script setup lang="ts">
import type { Product } from "../scripts/productType";
import ProductListItem from "./ProductListItemComponent.vue";

defineProps<{
  products: Product[];
}>();

defineEmits<{
  (e: "select-product", product: Product): void;
  (e: "update-product", product: Product): void;
  (e: "delete-product", productId: number): void;
}>();

</script>
<template>
  <h2>Liste des produits</h2>
  <div class="scroll-zone">
    <ul class="product-list">
      <ProductListItem
        v-for="product in products"
        :key="product.id"
        :product="product"
        @select-product="$emit('select-product', product)"
      />
    </ul>
  </div>
</template>
<style scoped>
.scroll-zone {
  max-height: 500px;
  overflow-y: auto;
  border: 1px solid rgba(255, 255, 255, 0.08); /* bordure douce */
  padding: 0.5rem;
  border-radius: 8px; /* coins arrondis */
  background-color: rgba(255, 255, 255, 0.03); /* léger fond transparent */
  backdrop-filter: blur(4px); /* effet verre dépoli subtil */
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15); /* ombre douce */
}

.product-list {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
