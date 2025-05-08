<script setup>
import { ref } from 'vue'

// Daftar kegiatan (to-do)
const todos = ref([
  { id: 1, text: 'Belajar VueJS', done: false },
  { id: 2, text: 'Kerjakan UTS PBK', done: true },
  { id: 3, text: 'Deploy ke Netlify', done: false }
])
</script>

<template>
  <main class="app-container">
    <h1>📋 Daftar Kegiatan</h1>

    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" :class="{ done: todo.done }">
        {{ todo.text }}
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

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-list li {
  background: white;
  margin: 0.5rem 0;
  padding: 1rem;
  border-radius: 8px;
  transition: 0.2s ease;
  border-left: 5px solid #42b883;
}

.todo-list li.done {
  text-decoration: line-through;
  color: #999;
  background-color: #e8e8e8;
  border-left-color: #888;
}
</style>
