<script setup>
import { ref, computed } from 'vue'

// Daftar kegiatan
const todos = ref([])

// Input dari user
const newTodo = ref('')

// Filter toggle
const showIncompleteOnly = ref(false)

// Tambah kegiatan
const addTodo = () => {
  if (newTodo.value.trim() !== '') {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value,
      done: false
    })
    newTodo.value = ''
  }
}

// Hapus kegiatan
const removeTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}

// Filter kegiatan
const filteredTodos = computed(() => {
  return showIncompleteOnly.value
    ? todos.value.filter(todo => !todo.done)
    : todos.value
})
</script>

<template>
  <main class="app-container">
    <h1>📋 Daftar Kegiatan</h1>

    <!-- Form -->
    <div class="form-group">
      <input v-model="newTodo" type="text" placeholder="Tambah kegiatan baru..." />
      <button @click="addTodo">Tambah</button>
    </div>

    <!-- Filter -->
    <div class="filter-group">
      <input type="checkbox" id="filter-incomplete" v-model="showIncompleteOnly" />
      <label for="filter-incomplete">Tampilkan yang belum selesai saja</label>
    </div>

    <!-- Daftar -->
    <ul class="todo-list">
      <li v-for="todo in filteredTodos" :key="todo.id" :class="{ done: todo.done }">
        <input type="checkbox" v-model="todo.done" class="checkbox" />
        <span class="todo-text">
          {{ todo.text }}
          <span v-if="todo.done" class="done-label">✅ Selesai</span>
        </span>
        <button class="delete-btn" @click="removeTodo(todo.id)">Hapus</button>
      </li>
    </ul>
  </main>
</template>

<!-- 🌍 Global style untuk body & background -->
<style>
body {
  margin: 0;
  padding: 0;
  background: url('https://images.unsplash.com/photo-1522202176988-66273c2fd55f?auto=format&fit=crop&w=1600&q=80') no-repeat center center fixed;
  background-size: cover;
  font-family: 'Segoe UI', sans-serif;
}
</style>

<!-- 🎨 Scoped style untuk komponen -->
<style scoped>
.app-container {
  max-width: 700px;
  margin: 3rem auto;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 16px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.25);
  backdrop-filter: blur(10px);
}

h1 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 1.5rem;
}

.form-group {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
  justify-content: center;
}

.filter-group {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  justify-content: center;
  margin-bottom: 1.5rem;
}

input[type="text"] {
  flex: 1;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
  background: #fefefe;
}

button {
  background-color: #42b883;
  color: white;
  padding: 0.75rem 1.25rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s ease;
}

button:hover {
  background-color: #369972;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-list li {
  background: white;
  margin: 0.5rem 0;
  padding: 1rem;
  border-radius: 8px;
  display: flex;
  align-items: center;
  border-left: 5px solid #42b883;
  transition: background 0.2s;
  gap: 0.75rem;
}

.todo-list li.done {
  text-decoration: line-through;
  color: #999;
  background-color: #e8e8e8;
  border-left-color: #888;
}

.todo-text {
  flex-grow: 1;
}

.done-label {
  margin-left: 0.5rem;
  font-size: 0.85rem;
  color: #42b883;
  font-weight: bold;
}

.checkbox {
  width: 1.2rem;
  height: 1.2rem;
  accent-color: #42b883;
}

.delete-btn {
  background-color: #ff4d4d;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 6px;
  color: white;
  font-size: 0.9rem;
  cursor: pointer;
}

.delete-btn:hover {
  background-color: #e60000;
}
</style>
