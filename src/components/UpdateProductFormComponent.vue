<script setup lang="ts">
</script>
<template>
  <div class="pt-4">
    <h3 class="pb-2">Modification du jeu vidéo</h3>
    <div>
      <div>
        <label for="product-id">ID du jeu vidéo:</label>
        <input
          type="text"
          v-model="newId"
          placeholder="ID du jeu vidéo"
          id="product-id"
        />
      </div>
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
          emit('update-product', {
            id: props.product.id,
            name: newName,
            description: newDescription,
            price: newPrice,
            stock: newStock,
          } as Product)
        "
      >
        Modifier le produit
      </button>
    </div>
  </div>
</template>
<style scoped></style>
