<template>
  <div class="app">
    <h1>{{ title }}</h1>

    <div class="input-group">
      <input 
        v-model="newItem" 
        type="text" 
        placeholder="Add a new item..."
        @keyup.enter="addItem"
      >
      <button @click="addItem">Add Item</button>
    </div>

    <div class="counter">
      Total Items: {{ items.length }}
    </div>

    <div class="items-list">
      <h2>Items:</h2>
      <div v-if="items.length === 0" class="empty-message">
        No items yet. Add one to get started!
      </div>
      <div v-for="(item, index) in items" :key="index" class="item">
        <span>{{ item }}</span>
        <button class="delete-btn" @click="removeItem(index)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const title = ref('My Simple List App')
const newItem = ref('')
const items = ref([])

const addItem = () => {
  if (newItem.value.trim() !== '') {
    items.value.push(newItem.value)
    newItem.value = ''
  }
}

const removeItem = (index) => {
  items.value.splice(index, 1)
}
</script>

<style scoped>
.app {
  background: white;
  border-radius: 10px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  padding: 40px;
  width: 100%;
  max-width: 500px;
}

h1 {
  color: #333;
  margin-bottom: 30px;
  text-align: center;
}

.input-group {
  margin-bottom: 20px;
}

input[type="text"] {
  width: 100%;
  padding: 12px;
  border: 2px solid #e0e0e0;
  border-radius: 5px;
  font-size: 16px;
  transition: border-color 0.3s;
  box-sizing: border-box;
}

input[type="text"]:focus {
  outline: none;
  border-color: #667eea;
}

button {
  width: 100%;
  padding: 12px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background 0.3s;
  margin-top: 10px;
}

button:hover {
  background: #764ba2;
}

.items-list {
  margin-top: 30px;
}

.items-list h2 {
  color: #333;
  font-size: 18px;
  margin-bottom: 15px;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  background: #f5f5f5;
  border-radius: 5px;
  margin-bottom: 10px;
}

.item span {
  color: #333;
}

.delete-btn {
  background: #ff6b6b;
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 3px;
  cursor: pointer;
  font-size: 14px;
  width: auto;
  margin: 0;
}

.delete-btn:hover {
  background: #ff5252;
}

.empty-message {
  text-align: center;
  color: #999;
  padding: 20px;
}

.counter {
  text-align: center;
  color: #667eea;
  font-size: 24px;
  font-weight: bold;
  margin: 20px 0;
}
</style>
