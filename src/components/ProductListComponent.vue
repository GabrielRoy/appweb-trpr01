<script setup lang="ts">
import type { Product } from "../models/product";
import { computed } from "vue";
import ProductListItem from "./ProductListItemComponent.vue";
import SearchQueryComponent from "./SearchQueryComponent.vue";
import { ref } from "vue";

const props = defineProps<{
  products: Product[];
}>();

defineEmits<{
  (e: "show-product", product: Product): void;
  (e: "update-product", product: Product): void;
  (e: "delete-product", productId: number): void;
  (e: "duplicate-product", product: Product): void;
  (e: "export-csv"): void;
}>();

const criticalStocks = computed(() =>
  props.products.filter((product: Product) => product.stock <= 3),
);

let searchQuery = ref<string>("");


const filteredProducts = computed(() => {
  const query = searchQuery.value.trim().toLowerCase();
  if (!query) return props.products;

  return props.products.filter((product: Product) =>
    product.name.toLowerCase().includes(query),
  );
});

</script>
<template>
  <h2>Liste des jeux vidéo</h2>
  <div class="list-zone">
    <SearchQueryComponent v-model="searchQuery" placeholder="Rechercher un jeu vidéo..." @update:searchQuery="searchQuery = $event" />
    <table class="product-list">
      <ProductListItem
        v-if="filteredProducts.length > 0"
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
        @show-product="$emit('show-product', product)"
        @update-product="$emit('update-product', product)"
        @delete-product="$emit('delete-product', product.id)"
        @duplicate-product="$emit('duplicate-product', product)"
      />
      <tr v-else>
        <td
          colspan="3"
          class="text-center p-4"
          style="color: rgba(255, 255, 255, 0.6)"
        >
          Aucun produit disponible pour le moment.
        </td>
      </tr>
    </table>
    <div class="export-container">
      <button class="btn-export" @click="$emit('export-csv')">
        Exporter CSV
      </button>
    </div>
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
.list-zone {
  border: 1px solid rgba(255, 255, 255, 0.08);
  padding: 0.5rem;
  border-radius: 8px;
  background-color: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(4px);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}

.product-list {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0 10px; /* espace entre les cartes */
}

.product-list td {
  padding: 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.product-list tr:hover {
  background: rgba(255, 255, 255, 0.05);
}

/* notifications */
.notification-field {
  background-color: #330000;
  color: #f44336;
  border: 1px solid #f44336;
  padding: 0.5rem 0.75rem;
  border-radius: 6px;
  margin-top: 1rem;
  font-weight: bold;
}

.notification-field ul {
  margin: 0;
  padding-left: 1.2rem;
}

.notification-field li {
  line-height: 1.3rem;
}

.btn-export {
  background: #22c55e;
  color: white;
  border: none;
  border-radius: 6px;
  padding: 6px 12px;
  cursor: pointer;
  font-weight: bold;
  margin-top: 1rem;
}

.btn-export:hover {
  background: #16a34a;
}
</style>
