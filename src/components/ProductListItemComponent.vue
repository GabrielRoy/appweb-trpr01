<script setup lang="ts">
import type { Product } from "../scripts/productType";
const props = defineProps<{
  product: Product;
}>();

function stockClass(stock: number) {
  if (stock > 20) return 'stock-high';
  if (stock > 10) return 'stock-medium';
  if (stock > 0) return 'stock-low';
  return 'stock-low';
}

</script>
<template>
  <li class="product-card" :class="stockClass(props.product.stock)">
    <div :class="`product-header`">
      <strong>{{ props.product.name }}</strong>
      <span class="product-id">#{{ props.product.id }}</span>
    </div>
    <p class="product-description">{{ product.description }}</p>
    <div class="product-footer">
      <span class="price"> Prix: {{ product.price }} $</span>
      <span class="stock"> Stock: {{ product.stock }}</span>
    </div>
  </li>
</template>
<style scoped>
.product-card {
    text-decoration: none;
  background: white;
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 10px;
  margin-bottom: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.product-header {
  display: flex;
  justify-content: space-between;
  font-size: 1.1em;
  margin-bottom: 5px;
}

.product-id {
  color: #888;
}

.product-description {
  font-size: 0.9em;
  color: #555;
  margin-bottom: 8px;
}

.product-footer {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
}

.price {
  color: #2a9d8f;
}

.stock {
  color: #e76f51;
}

.stock-high {
  background-color: rgba(76, 175, 80, 0.12); /* vert sombre transparent */
  border: 1px solid rgba(76, 175, 80, 0.4);  /* vert plus clair */
}

.stock-medium {
  background-color: rgba(255, 235, 59, 0.12); /* jaune sombre transparent */
  border: 1px solid rgba(255, 235, 59, 0.4);  /* jaune plus clair */
}

.stock-low {
  background-color: rgba(244, 67, 54, 0.12); /* rouge sombre transparent */
  border: 1px solid rgba(244, 67, 54, 0.4);  /* rouge plus clair */
}

</style>
