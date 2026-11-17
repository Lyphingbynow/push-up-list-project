<template>
  <section class="list-app">
    <h2>My list</h2>
    <form @submit.prevent="addItem">
      <input v-model="newItem" type="text" placeholder="Enter an item" aria-label="New list item" />
      <button type="submit">Add item</button>
    </form>

    <p v-if="items.length === 0">Your list is empty.</p>
    <ul v-else>
      <li v-for="item in items" :key="item.id">
        <span>{{ item.text }}</span>
        <button type="button" @click="removeItem(item.id)">Delete</button>
      </li>
    </ul>
    <p>Items: {{ itemCount }}</p>
  </section>
</template>

<script setup>
import { computed, ref } from 'vue'

const newItem = ref('')
const items = ref([])
let nextId = 1

const itemCount = computed(() => items.value.length)

function addItem() {
  const text = newItem.value.trim()
  if (!text) return

  items.value.push({ id: nextId++, text })
  newItem.value = ''
}

function removeItem(id) {
  items.value = items.value.filter((item) => item.id !== id)
}
</script>

<style scoped>
.list-app {
  max-width: 420px;
  margin: 2rem auto;
  font-family: sans-serif;
}

form,
li {
  display: flex;
  gap: 0.5rem;
}

input {
  flex: 1;
  min-width: 0;
  padding: 0.5rem;
}

button {
  padding: 0.5rem 0.75rem;
  cursor: pointer;
}

ul {
  padding: 0;
  list-style: none;
}

li {
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 0;
  border-bottom: 1px solid #ddd;
}
</style>