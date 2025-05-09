<script setup>
import { ref } from 'vue'

// Daftar kegiatan (to-do)
const todos = ref([
  { id: 1, text: 'Belajar VueJS', done: false },
  { id: 2, text: 'Kerjakan UTS PBK', done: true },
  { id: 3, text: 'Deploy ke Netlify', done: false }
])

// Input dari user
const newTodo = ref('')

// Fungsi menambah kegiatan
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

// Fungsi menghapus kegiatan
const removeTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}
</script>

<template>
  <main class="app-container">
    <h1>📋 Daftar Kegiatan</h1>

    <!-- Form Tambah Kegiatan -->
    <div class="form-group">
      <input v-model="newTodo" type="text" placeholder="Tambah kegiatan baru..." />
      <button @click="addTodo">Tambah</button>
    </div>

    <!-- Daftar Kegiatan -->
    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" :class="{ done: todo.done }">
        {{ todo.text }}
        <button class="delete-btn" @click="removeTodo(todo.id)">Hapus</button>
      </li>
    </ul>
  </main>
</template>

<style scoped>
.app-container {
  max-width: 600px;
  margin: auto;
  padding: 2rem;
  font-family: 'Segoe UI', sans-serif;
  background: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 1.5rem;
}

.form-group {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  justify-content: center;
}

input[type="text"] {
  flex: 1;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
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
  justify-content: space-between;
  align-items: center;
  border-left: 5px solid #42b883;
}

.todo-list li.done {
  text-decoration: line-through;
  color: #999;
  background-color: #e8e8e8;
  border-left-color: #888;
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
