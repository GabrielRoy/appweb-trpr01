<script setup lang="ts">
import { ref } from "vue";
import type { Product } from "../scripts/product";

const emit = defineEmits<{
  (e: "create-product", newProduct: Product): void;
}>();

const nextId = ref(1);
let newName = ref<string>("");
let newDescription = ref<string>("");
let newPrice = ref<number>(0);
let newStock = ref<number>(0);

const errors = ref<string[]>([]);

//Créer à l'aide de l'IA
const createProduct = () => {
  errors.value = []; // reset

  // Validation
  if (!newName.value.trim())
    errors.value.push("Le nom du jeu vidéo est requis.");
  if (!newDescription.value.trim())
    errors.value.push("La description est requise.");
  if (newPrice.value < 0)
    errors.value.push("Le prix doit être supérieur ou égal à 0.");
  if (newStock.value < 0)
    errors.value.push("Le stock doit être supérieur ou égal à 0.");

  if (errors.value.length > 0) return; // stop si erreurs

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
    <div>
      <div>
        <label for="product-name">Nom du jeu vidéo:</label>
        <input
          type="text"
          v-model="newName"
          placeholder="Nom du jeu vidéo"
          id="product-name"
        />
      </div>
      <div>
        <label for="product-description">Description du jeu vidéo:</label>
        <input
          type="text"
          v-model="newDescription"
          placeholder="Description du jeu vidéo"
          id="product-description"
        />
      </div>
      <div>
        <label for="product-price">Prix du jeu vidéo:</label>
        <input
          type="number"
          v-model="newPrice"
          placeholder="Prix du jeu vidéo"
          id="product-price"
        />
      </div>
      <div>
        <label for="product-stock">Stock du jeu vidéo:</label>
        <input
          type="number"
          v-model="newStock"
          placeholder="Stock du jeu vidéo"
          id="product-stock"
        />
      </div>
      <button
        @click="
          createProduct()
        "
      >
        Ajouter le produit
      </button>
      <div v-if="errors.length" class="error-field">
        <ul>
          <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
        </ul>
      </div>
    </div>
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
