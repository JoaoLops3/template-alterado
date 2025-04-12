<script setup>
import { ref } from 'vue'

const isDark = ref(false)

const toggleTheme = () => {
  isDark.value = !isDark.value
  document.body.classList.toggle('dark-theme')
}
</script>

<template>
  <button @click="toggleTheme" class="theme-toggle">
    {{ isDark ? '☀️' : '🌙' }}
  </button>
</template>

<style scoped>
.theme-toggle {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 10px;
  font-size: 20px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  z-index: 1000;
  border-radius: 50%;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s;
}

.theme-toggle:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

:global(.dark-theme) .theme-toggle:hover {
  background-color: rgba(255, 255, 255, 0.1);
}
</style> 