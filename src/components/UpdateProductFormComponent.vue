<script setup lang="ts">
import { ref } from "vue";
import type { Product } from "../models/product";

const props = defineProps<{
  product: Product;
}>();

const emit = defineEmits<{
  (e: "update-product", updatedProduct: Product): void;
  (e: "cancel"): void;
}>();

const newName = ref<string>(props.product.name);
const newDescription = ref<string>(props.product.description);
const newPrice = ref<number>(props.product.price);
const newStock = ref<number>(props.product.stock);

const errorsName = ref("");
const errorsDescription = ref("");
const errorsPrice = ref("");
const errorsStock = ref("");

const updateProduct = () => {
  // reset erreurs
  errorsName.value = "";
  errorsDescription.value = "";
  errorsPrice.value = "";
  errorsStock.value = "";

  // Validation
  if (!newName.value.trim())
    errorsName.value = "Le nom du jeu vidéo est requis.";
  if (!newDescription.value.trim())
    errorsDescription.value = "La description est requise.";
  if (newPrice.value < 0)
    errorsPrice.value = "Le prix doit être supérieur ou égal à 0.";
  if (newStock.value < 0)
    errorsStock.value = "Le stock doit être supérieur ou égal à 0.";

  // Stop si au moins une erreur
  if (
    errorsName.value ||
    errorsDescription.value ||
    errorsPrice.value ||
    errorsStock.value
  )
    return;

  // Emit update
  emit("update-product", {
    id: props.product.id,
    name: newName.value,
    description: newDescription.value,
    price: newPrice.value,
    stock: newStock.value,
  });
};
</script>
<template>
  <div class="pt-4">
    <h3 class="pb-2">Modification du jeu vidéo</h3>

    <div class="mb-3">
      <label for="product-name" class="form-label">Nom du jeu vidéo:</label>
      <input
        type="text"
        v-model="newName"
        placeholder="Nom du jeu vidéo"
        id="product-name"
        class="form-control"
        :class="{ 'is-invalid': errorsName }"
      />
      <div v-if="errorsName" class="invalid-feedback">
        {{ errorsName }}
      </div>
    </div>

    <div class="mb-3">
      <label for="product-description" class="form-label"
        >Description du jeu vidéo:</label
      >
      <input
        type="text"
        v-model="newDescription"
        placeholder="Description du jeu vidéo"
        id="product-description"
        class="form-control"
        :class="{ 'is-invalid': errorsDescription }"
      />
      <div v-if="errorsDescription" class="invalid-feedback">
        {{ errorsDescription }}
      </div>
    </div>

    <div class="mb-3">
      <label for="product-price" class="form-label">Prix du jeu vidéo:</label>
      <input
        type="number"
        v-model="newPrice"
        placeholder="Prix du jeu vidéo"
        id="product-price"
        class="form-control"
        :class="{ 'is-invalid': errorsPrice }"
      />
      <div v-if="errorsPrice" class="invalid-feedback">
        {{ errorsPrice }}
      </div>
    </div>

    <div class="mb-3">
      <label for="product-stock" class="form-label">Stock du jeu vidéo:</label>
      <input
        type="number"
        v-model="newStock"
        placeholder="Stock du jeu vidéo"
        id="product-stock"
        class="form-control"
        :class="{ 'is-invalid': errorsStock }"
      />
      <div v-if="errorsStock" class="invalid-feedback">
        {{ errorsStock }}
      </div>
    </div>

    <button @click="updateProduct()" class="btn btn-primary me-2">
      Modifier le produit
    </button>
    <button @click="$emit('cancel')" class="btn btn-cancel">Annuler</button>
  </div>
</template>
<style scoped>
.pt-4 {
  padding: 1.5rem;
  max-width: 500px;
  margin: auto;
  background: #1e1e1e;
  border-radius: 12px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

h3 {
  margin-bottom: 1.2rem;
  font-size: 1.4rem;
  color: #ffffff;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  padding-bottom: 0.5rem;
}

.pt-4 > div > div {
  display: flex;
  flex-direction: column;
  margin-bottom: 1rem;
}

label {
  font-weight: 500;
  margin-bottom: 0.4rem;
  font-size: 0.9rem;
  color: #bbbbbb;
}

input {
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #333;
  background-color: #2a2a2a;
  color: #ffffff;
  font-size: 0.95rem;
  transition: all 0.2s ease;
}

input::placeholder {
  color: #777;
}

input:focus {
  outline: none;
  border-color: #3b82f6;
  box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.3);
}

button {
  width: 100%;
  padding: 11px;
  margin-top: 0.8rem;
  border: none;
  border-radius: 8px;
  background: linear-gradient(135deg, #3b82f6, #2563eb);
  color: white;
  font-weight: 600;
  font-size: 0.95rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

button:hover {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  transform: translateY(-2px);
}

button:active {
  transform: scale(0.98);
}
.error-field {
  margin-top: 1rem;
  background-color: #330000;
  color: #f44336;
  border: 1px solid #f44336;
  padding: 0.5rem 0.75rem;
  border-radius: 6px;
  margin-bottom: 1rem;
  font-weight: bold;
}

.error-field ul {
  margin: 0;
  padding-left: 1.2rem;
}

.error-field li {
  line-height: 1.3rem;
}

.btn-cancel {
  background: linear-gradient(135deg, #ef4444, #dc2626);
  color: white;
}

.btn-cancel:hover {
  background: linear-gradient(135deg, #dc2626, #b91c1c);
  transform: translateY(-2px);
}
</style>
