<script setup lang="ts">
import { ref } from "vue";
import type { Product } from "../models/product";

const emit = defineEmits<{
  (e: "create-product", newProduct: Product): void;
}>();

const nextId = ref(1);
let newName = ref<string>("");
let newDescription = ref<string>("");
let newPrice = ref<number>(0);
let newStock = ref<number>(0);

const errorsName = ref("");
const errorsDescription = ref("");
const errorsPrice = ref("");
const errorsStock = ref("");

const createProduct = () => {
  // reset erreurs
  errorsName.value = "";
  errorsDescription.value = "";
  errorsPrice.value = "";
  errorsStock.value = "";

  // Validation
  if (!newName.value.trim() || newName.value.trim().length < 3)
    errorsName.value =
      "Le nom du jeu vidéo est requis avec 3 caractères minimum.";

  if (!newDescription.value.trim())
    errorsDescription.value = "La description est requise.";

  if (newPrice.value < 0)
    errorsPrice.value = "Le prix doit être supérieur ou égal à 0.";
  else if (!Number.isInteger(newPrice.value * 100))
    errorsPrice.value = "Le prix ne peut pas avoir plus de deux décimales.";

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

  // Création du produit
  emit("create-product", {
    id: nextId.value,
    name: newName.value,
    description: newDescription.value,
    price: newPrice.value,
    stock: newStock.value,
  });

  nextId.value += 1;

  // Reset des champs
  newName.value = "";
  newDescription.value = "";
  newPrice.value = 0;
  newStock.value = 0;
};

//Donné par l'IA
//Je sais que cela permet d'envoyer au ref des données a partir des parents
defineExpose({
  newName,
  newDescription,
  newPrice,
  newStock,
});
</script>
<template>
  <div class="pt-4">
    <h3 class="pb-2">Création de jeu vidéo</h3>
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

    <button class="btn btn-primary" @click="createProduct()">
      Ajouter le jeu vidéo
    </button>
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
</style>
