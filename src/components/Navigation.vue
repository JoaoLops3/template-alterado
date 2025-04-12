<script setup>
import { ref } from 'vue'

const emit = defineEmits(['update:currentPage'])
const props = defineProps({
  currentPage: {
    type: String,
    required: true
  }
})

const navigateTo = (page) => {
  emit('update:currentPage', page)
}
</script>

<template>
  <nav class="navigation">
    <button 
      @click="navigateTo('todo')" 
      :class="{ active: currentPage === 'todo' }"
      class="nav-button"
    >
      Lista de Tarefas
    </button>
    <button 
      @click="navigateTo('pomodoro')" 
      :class="{ active: currentPage === 'pomodoro' }"
      class="nav-button"
    >
      Pomodoro
    </button>
  </nav>
</template>

<style scoped>
.navigation {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-bottom: 30px;
  padding: 15px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.nav-button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background-color: #f0f0f0;
  color: #2c3e50;
  cursor: pointer;
  transition: all 0.3s;
  font-size: 1rem;
}

.nav-button:hover {
  background-color: #e0e0e0;
}

.nav-button.active {
  background-color: #42b883;
  color: white;
}
</style> 