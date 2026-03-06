<script setup lang="ts">
import type { Product } from "../scripts/product";
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
  <tr
    class="product-card"
    :class="stockClass(props.product.stock)"
    @click="$emit('show-product', props.product)"
  >
    <td class="product-cell">
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

          <button
            class="duplicate-btn"
            @click.stop="$emit('duplicate-product', props.product)"
          >
            Dupliquer
          </button>
        </div>
      </div>
    </td>
  </tr>
</template>
<style scoped>
.product-card td {
  padding: 0;
  border: none;
}

/* cellule contenant la carte */
.product-cell {
  width: 100%;
  padding: 12px;
  border-radius: 8px;
  overflow: hidden;
  box-sizing: border-box;
}

/* CARTE PRODUIT */
.product-card > td {
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 8px;
  padding: 12px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.15);
  cursor: pointer;
  transition: transform 0.15s ease, background 0.15s ease;
}

.product-card:hover > td {
  transform: scale(1.01);
  background: rgba(255,255,255,0.06);
}

/* HEADER */
.product-header {
  display: flex;
  justify-content: space-between;
  font-size: 1.05em;
  margin-bottom: 6px;
}

.product-id {
  color: rgba(255,255,255,0.5);
  font-size: 0.85em;
}

/* DESCRIPTION */
.product-description {
  font-size: 0.9em;
  color: rgba(255,255,255,0.7);
  margin-bottom: 10px;
}

/* FOOTER ALIGNEMENT */
.product-footer {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  margin-top: 10px;
}

/* PRIX */
.price {
  font-weight: bold;
  color: #2dd4bf;
}

/* STOCK */
.stock {
  justify-self: center;
  font-weight: bold;
  color: #fb7185;
}

/* ACTIONS */
.product-actions {
  display: flex;
  gap: 6px;
}

/* BOUTONS */
button {
  padding: 4px 9px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 0.8em;
  transition: 0.15s;
}

/* Modifier */
.btn-update {
  background: #3b82f6;
  color: white;
}

.btn-update:hover {
  background: #2563eb;
}

/* Supprimer */
.btn-delete {
  background: #ef4444;
  color: white;
}

.btn-delete:hover {
  background: #dc2626;
}

/* Dupliquer */
.duplicate-btn {
  background: #f59e0b;
  color: white;
  font-weight: 600;
}

.duplicate-btn:hover {
  background: #d97706;
}

/* COULEURS STOCK */

.stock-high > td {
  background: rgba(34,197,94,0.12);
  border: 1px solid rgba(34,197,94,0.35);
}

.stock-medium > td {
  background: rgba(250,204,21,0.12);
  border: 1px solid rgba(250,204,21,0.35);
}

.stock-low > td {
  background: rgba(239,68,68,0.12);
  border: 1px solid rgba(239,68,68,0.35);
}
</style>
