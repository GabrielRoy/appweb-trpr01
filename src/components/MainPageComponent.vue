<script setup lang="ts">
import AddProductForm from "./AddProductFormComponent.vue";
import type { Product } from "../models/product";
import ProductList from "./ProductListComponent.vue";
import ShowProduct from "./ShowProduct.vue";
import { ref } from "vue";
import UpdateProductForm from "./UpdateProductFormComponent.vue";

let products = ref<Product[]>([]);

let selectedProduct = ref<Product | null>(null);

let isUpdatingProduct = ref<boolean>(false);

let productToUpdate = ref<Product | null>(null);

let errorMessages = ref<string[]>([]);

let confirmationMessage = ref<string[]>([]);

function addProduct(product: Product) {
  products.value.push(product);
  confirmationMessage.value.push(
    `Le produit "${product.name}" a été ajouté avec succès.`,
  );
}

function deleteProduct(id: number) {
  products.value = products.value.filter(
    (product: Product) => product.id !== id,
  );
  confirmationMessage.value.push(
    `Le produit avec l'id ${id} a été supprimé avec succès.`,
  );
}

function updateProduct(updatedProduct: Product) {
  const product: Product | undefined = products.value.find(
    (product: Product) => product.id === updatedProduct.id,
  );

  if (product) {
    product.name = updatedProduct.name;
    product.description = updatedProduct.description;
    product.price = updatedProduct.price;
    product.stock = updatedProduct.stock;

    confirmationMessage.value.push(
      `Le produit "${updatedProduct.name}" a été mis à jour avec succès.`,
    );
  } else {
    //Cela pourrait arriver, mais il y a très peu de chance.
    errorMessages.value.push(
      `Le produit avec l'id ${updatedProduct.id} n'a pas été trouvé.`,
    );
    console.error(`Product with id ${updatedProduct.id} not found.`);
  }

  isUpdatingProduct.value = false;
}

//Codé par l'IA
function exportProductsInCSV() {
  if (!products.value.length) return;

  // 1️⃣ Créer l'en-tête CSV
  const headers = ["ID", "Nom", "Description", "Prix", "Stock"];
  const csvRows = [headers.join(",")];

  // 2️⃣ Ajouter les lignes des produits
  products.value.forEach(product => {
    const row = [
      product.id,
      `"${product.name.replace(/"/g, '""')}"`,         // échappe les guillemets
      `"${product.description.replace(/"/g, '""')}"`,
      product.price,
      product.stock
    ];
    csvRows.push(row.join(","));
  });

  // 3️⃣ Générer le CSV complet
  const csvString = csvRows.join("\n");

  // 4️⃣ Créer un blob et déclencher le téléchargement
  const blob = new Blob([csvString], { type: "text/csv;charset=utf-8;" });
  const link = document.createElement("a");
  link.href = URL.createObjectURL(blob);
  link.download = "produits.csv";
  link.style.display = "none";
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
}

function showProduct(product: Product) {
  selectedProduct.value = product;
}

function productToUpdateClick(product: Product) {
  productToUpdate.value = product;
  isUpdatingProduct.value = true;
}

//Codé par l'IA
// Ref pour accéder au formulaire
const addProductForm = ref<any>(null);
// Fonction pour remplir le formulaire
const duplicateProduct = (product: Product) => {
  if (!addProductForm.value) return; // sécurité
  addProductForm.value.newName = product.name;
  addProductForm.value.newDescription = product.description;
  addProductForm.value.newPrice = product.price;
  addProductForm.value.newStock = product.stock;
};
</script>

<template>
  <h2>Système d'inventaire du magasin</h2>
  <div>
    <div v-if="!isUpdatingProduct">
      <AddProductForm ref="addProductForm" @create-product="addProduct" />
    </div>
    <div v-if="isUpdatingProduct">
      <UpdateProductForm
        v-bind:product="productToUpdate!"
        @update-product="updateProduct"
        @cancel="isUpdatingProduct = false"
      />
    </div>

    <div>
      <ProductList
      :products="products"
      @delete-product="deleteProduct"
      @show-product="showProduct"
      @update-product="productToUpdateClick"
      @duplicate-product="duplicateProduct"
      @export-csv="exportProductsInCSV"
      />
    </div>

    <div v-if="selectedProduct">
      <h2>Description du produit selectionné</h2>
      <div v-if="selectedProduct">
        <ShowProduct :product="selectedProduct" />
      </div>
    </div>
  </div>
</template>

<style scoped>
div > div {
  margin-bottom: 2rem; /* ajustable selon le besoin */
}

/* Optionnel : titre */
h2 {
  margin-bottom: 1.5rem;
  color: #fff; /* si thème sombre */
}

/* Si tu veux plus de style dark pour le conteneur principal */
div {
  color: #fff;
  font-family: "Segoe UI", sans-serif;
}
</style>
