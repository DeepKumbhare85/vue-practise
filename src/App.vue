<script setup>
import { ref } from 'vue';
import AppTable from './components/AppTable.vue';

const rows = [
  { id: 1, name: 'Deep', age: 21, email: 'deep@email.com' },
  { id: 2, name: 'Heet', age: 22, email: 'heet@email.com' },
  { id: 3, name: 'Sanket', age: 21, email: 'sanket@email.com' },
];

const cols = ref([
  { key: 'id' },
  { key: 'name' },
  { key: 'age' },
  { key: 'email' },
]);



</script>

<template>
  <AppTable :items="rows" :cols="cols" :search="false">
    <template #col-id="{ item }">
      My ID {{ item.id }}
    </template>
  </AppTable>
</template>

<style scoped></style>
