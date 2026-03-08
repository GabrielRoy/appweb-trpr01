<script setup lang="ts">
const props = defineProps<{
  modelValue: string;
  placeholder: string;
}>();

const emit = defineEmits<{
  (e: "update:searchQuery", value: string): void;
}>();

</script>
<template>
  <input
    type="text"
    class="search-input"
    :placeholder="placeholder"
    :value="modelValue"
    @input="$emit('update:searchQuery', ($event.target as HTMLInputElement).value)"
  />
</template>
<style scoped>
.search-input {
  width: 100%;
  padding: 8px;
  margin-bottom: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>