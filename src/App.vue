<script setup>
import TodoList from './components/TodoList.vue'
import PomodoroTimer from './components/PomodoroTimer.vue'
import Navigation from './components/Navigation.vue'
import ThemeToggle from './components/ThemeToggle.vue'
import { ref } from 'vue'

const currentPage = ref('todo')
</script>

<template>
  <div class="app">
    <ThemeToggle />
    <h1>Minha Aplicação Vue</h1>
    <Navigation v-model:currentPage="currentPage" />
    <TodoList v-if="currentPage === 'todo'" />
    <PomodoroTimer v-if="currentPage === 'pomodoro'" />
  </div>
</template>

<style>
:root {
  --bg-color: #ffffff;
  --text-color: #2c3e50;
  --card-bg: #f5f5f5;
  --card-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  --input-bg: #ffffff;
  --input-border: #ddd;
}

.dark-theme {
  --bg-color: #1a1a1a;
  --text-color: #ffffff;
  --card-bg: #2d2d2d;
  --card-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  --input-bg: #3d3d3d;
  --input-border: #4d4d4d;
}

body {
  margin: 0;
  background-color: var(--bg-color);
  color: var(--text-color);
  transition: background-color 0.3s, color 0.3s;
}

.app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  color: var(--text-color);
  margin-bottom: 30px;
}

/* Estilos globais para componentes */
.todo-container,
.pomodoro-container,
.navigation {
  background-color: var(--card-bg) !important;
  box-shadow: var(--card-shadow) !important;
}

input,
button {
  background-color: var(--input-bg);
  border-color: var(--input-border);
  color: var(--text-color);
}

.todo-item {
  background-color: var(--input-bg) !important;
}

.todo-text {
  color: var(--text-color) !important;
}
</style>
