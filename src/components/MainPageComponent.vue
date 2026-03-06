<script setup lang="ts">
import AddProductForm from "./AddProductFormComponent.vue";
import type { Product } from "../scripts/product";
import ProductList from "./ProductListComponent.vue";
import ShowProduct from "./ShowProduct.vue";
import { ref } from "vue";
import UpdateProductForm from "./UpdateProductFormComponent.vue";

let products = ref<Product[]>([
  {
    id: 1,
    name: "Produit 1",
    price: 10.99,
    description: "Description du Produit 1",
    stock: 100,
  },
  {
    id: 2,
    name: "Produit 2",
    price: 19.99,
    description: "Description du Produit 2",
    stock: 100,
  },
  {
    id: 3,
    name: "Produit 3",
    price: 29.99,
    description: "Description du Produit 3",
    stock: 50,
  },
  {
    id: 4,
    name: "Produit 4",
    price: 39.99,
    description: "Description du Produit 4",
    stock: 75,
  },
  {
    id: 5,
    name: "Produit 5",
    price: 49.99,
    description: "Description du Produit 5",
    stock: 25,
  },
]);

let searchQuery = ref<string>("");

let selectedProduct = ref<Product | null>({
  id: 1,
  name: "Produit Test",
  description: "Description du produit test",
  price: 25.0,
  stock: 10,
});

let isUpdatingProduct = ref<boolean>(false);

let productToUpdate = ref<Product | null>({
  id: 1,
  name: "Produit Test",
  description: "Description du produit test",
  price: 25.0,
  stock: 10,
});

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
}

function exportProductsInCSV() {
  //TODO: Implémenter l'exportation des produits en CSV
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
  <h2>Système de Gestion de Produits</h2>
  <div>
    
    <div v-if="!isUpdatingProduct">
      <AddProductForm ref="addProductForm" @create-product="addProduct" />
    </div>
    <div v-if="isUpdatingProduct">
      <UpdateProductForm
      v-bind:product="productToUpdate!"
      @update-product="updateProduct"
      />
    </div>
    
    <div>
      <ProductList
        :products="products"
        @delete-product="deleteProduct"
        @show-product="showProduct"
        @update-product="productToUpdateClick"
        @duplicate-product="duplicateProduct"
      />
    </div>

    <h2>Description du produit selectionné</h2>
    <div v-if="selectedProduct">
      <ShowProduct :product="selectedProduct" />
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
