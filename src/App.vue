<script setup>
import { ref } from 'vue';
import AppTable from './components/AppTable.vue';

const rows = [
  // { id: 1, name: 'Deep', age: 21, email: 'deep@email.com' },
  // { id: 2, name: 'Heet', age: 22, email: 'heet@email.com' },
  // { id: 3, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 4, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 5, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 6, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 7, name: 'Deep', age: 21, email: 'sanket@email.com' },
  // { id: 8, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 9, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 10, name: 'heet', age: 21, email: 'sanket@email.com' },
  // { id: 11, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 12, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 13, name: 'Deep', age: 21, email: 'sanket@email.com' },
  // { id: 14, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 15, name: 'heet', age: 21, email: 'sanket@email.com' },
  // { id: 16, name: 'Harsh', age: 21, email: 'sanket@email.com' },
  // { id: 17, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 18, name: 'Deep', age: 21, email: 'sanket@email.com' },
  // { id: 19, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 19, name: 'Sanket', age: 21, email: 'sanket@email.com' },
  // { id: 19, name: 'Sanket', age: 21, email: 'sanket@email.com' },
];

const cols = ref([
  { key: 'id' },
  { key: 'name' },
  { key: 'age' },
  { key: 'email' },
]);



</script>

<template>
  <AppTable :items="rows" :cols="cols" :search="false" no-data-text="No data available">
    <template #col-id="{ item }">
      My ID {{ item.id }}
    </template>
  </AppTable>
</template>

<style scoped></style>
