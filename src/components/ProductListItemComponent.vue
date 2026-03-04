<script setup lang="ts">
import type { Product } from "../scripts/productType";
const props = defineProps<{
  product: Product;
}>();

function stockClass(stock: number) {
  if (stock > 20) return "stock-high";
  if (stock > 10) return "stock-medium";
  if (stock > 0) return "stock-low";
  return "stock-low";
}

defineEmits<{
  (e: "show-product", product: Product): void;
  (e: "update-product", product: Product): void;
  (e: "delete-product", productId: number): void;
  (e: "duplicate-product", product: Product): void;
}>();
</script>
<template>
  <li
    class="product-card"
    :class="stockClass(props.product.stock)"
    @click="$emit('show-product', props.product)"
  >
    <div class="product-header">
      <strong>{{ props.product.name }}</strong>
      <span class="product-id">#{{ props.product.id }}</span>
    </div>

    <p class="product-description">
      {{ props.product.description }}
    </p>

    <div class="product-footer">
      <span class="price">Prix: {{ props.product.price }} $</span>
      <span class="stock">Stock: {{ props.product.stock }}</span>

      <div class="product-actions">
        <button
          class="btn-update"
          @click.stop="$emit('update-product', props.product)"
        >
          Modifier
        </button>
        <button
          class="btn-delete"
          @click.stop="$emit('delete-product', props.product.id)"
        >
          Supprimer
        </button>
        <button class="duplicate-btn" @click.stop="$emit('duplicate-product', props.product)">
          Dupliquer
        </button>
      </div>
    </div>
  </li>
</template>
<style scoped>
.product-card {
  text-decoration: none;
  background: white;
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 12px;
  margin-bottom: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  cursor: pointer;
  transition: transform 0.1s ease;
}

.product-card:hover {
  transform: scale(1.01);
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
  margin-bottom: 10px;
}

/* -------- FOOTER ALIGNEMENT PARFAIT -------- */

.product-footer {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  margin-top: 12px;
}

/* PRIX - gauche */
.price {
  font-weight: bold;
  color: #2a9d8f;
}

/* STOCK - parfaitement centré */
.stock {
  justify-self: center;
  font-weight: bold;
  color: #e76f51;
}

/* BOUTONS - droite */
.product-actions {
  display: flex;
  gap: 8px;
}

.product-actions .duplicate-btn {
  background-color: #f59e0b; /* couleur orange pour différencier */
  color: white;
  border: none;
  border-radius: 6px;
  padding: 5px 10px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.product-actions .duplicate-btn:hover {
  background-color: #d97706; /* orange plus foncé au survol */
}

/* Boutons */
button {
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.85em;
}

.btn-update {
  background-color: #2196f3;
  color: white;
}

.btn-delete {
  background-color: #f44336;
  color: white;
}

/* -------- COULEURS STOCK -------- */

.stock-high {
  background-color: rgba(76, 175, 80, 0.12);
  border: 1px solid rgba(76, 175, 80, 0.4);
}

.stock-medium {
  background-color: rgba(255, 235, 59, 0.12);
  border: 1px solid rgba(255, 235, 59, 0.4);
}

.stock-low {
  background-color: rgba(244, 67, 54, 0.12);
  border: 1px solid rgba(244, 67, 54, 0.4);
}
</style>
