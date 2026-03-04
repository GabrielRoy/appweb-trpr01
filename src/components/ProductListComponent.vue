<script setup lang="ts">
import type { Product } from "../scripts/productType";
import { computed } from "vue";
import ProductListItem from "./ProductListItemComponent.vue";

const props = defineProps<{
  products: Product[];
}>();

defineEmits<{
  (e: "show-product", product: Product): void;
  (e: "update-product", product: Product): void;
  (e: "delete-product", productId: number): void;
  (e: "duplicate-product", product: Product): void;
}>();

const criticalStocks = computed(() =>
  props.products.filter((product: Product) => product.stock <= 3),
);
</script>
<template>
  <h2>Liste des produits</h2>
  <div class="scroll-zone">
    <ul class="product-list">
      <ProductListItem
        v-for="product in products"
        :key="product.id"
        :product="product"
        @show-product="$emit('show-product', product)"
        @update-product="$emit('update-product', product)"
        @delete-product="$emit('delete-product', product.id)"
        @duplicate-product="$emit('duplicate-product', product)"
      />
    </ul>
  </div>

  <!--Générer par l'IA-->
  <div v-if="criticalStocks.length" class="notification-field">
    <ul>
      <li v-for="product in criticalStocks" :key="product.id">
        ⚠️ Stock critique pour "{{ product.name }}" :
        {{ product.stock }} restant
      </li>
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

.notification-field {
  background-color: #330000;
  color: #f44336;
  border: 1px solid #f44336;
  padding: 0.5rem 0.75rem;
  border-radius: 6px;
  margin-top: 1rem; /* espace avec la liste */
  font-weight: bold;
}

.notification-field ul {
  margin: 0;
  padding-left: 1.2rem;
}

.notification-field li {
  line-height: 1.3rem;
}
</style>
