<script setup>
import { ref, computed } from 'vue';
const list = ref([]);
const removelist = ref([]);
function addItem(item) {
  list.value.push(item);
}
function removeItem(item) {
  const index = list.value.indexOf(item);
  if (index > -1) {
    list.value.splice(index, 1);
  }
}
computed(() => {
  removelist.value = list.value.filter(item => item.shouldRemove);
});
</script>
<template>
  <input v-model="newItem" placeholder="Add item" @keyup.enter="addItem(newItem)" />
  <ul>
    <li v-for="item in list" :key="item.id">
      {{ item.name }}
      <button @click="removeItem(item)">Remove</button>
    </li>
  </ul>
</template>
