<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const timeLeft = ref(25 * 60) // 25 minutos em segundos
const isRunning = ref(false)
const isBreak = ref(false)
const timer = ref(null)

const minutes = computed(() => {
  return Math.floor(timeLeft.value / 60)
})

const seconds = computed(() => {
  return timeLeft.value % 60
})

const formattedTime = computed(() => {
  return `${minutes.value.toString().padStart(2, '0')}:${seconds.value.toString().padStart(2, '0')}`
})

const startTimer = () => {
  if (!isRunning.value) {
    isRunning.value = true
    timer.value = setInterval(() => {
      if (timeLeft.value > 0) {
        timeLeft.value--
      } else {
        clearInterval(timer.value)
        isRunning.value = false
        isBreak.value = !isBreak.value
        timeLeft.value = isBreak.value ? 5 * 60 : 25 * 60 // 5 minutos de pausa, 25 de trabalho
      }
    }, 1000)
  }
}

const pauseTimer = () => {
  if (isRunning.value) {
    clearInterval(timer.value)
    isRunning.value = false
  }
}

const resetTimer = () => {
  clearInterval(timer.value)
  isRunning.value = false
  isBreak.value = false
  timeLeft.value = 25 * 60
}

onUnmounted(() => {
  clearInterval(timer.value)
})
</script>

<template>
  <div class="pomodoro-container">
    <h2>Técnica Pomodoro</h2>
    <div class="timer-display" :class="{ 'break-time': isBreak }">
      {{ formattedTime }}
    </div>
    <div class="timer-status">
      {{ isBreak ? 'Pausa' : 'Tempo de Trabalho' }}
    </div>
    <div class="controls">
      <button @click="startTimer" :disabled="isRunning" class="control-button start">
        Iniciar
      </button>
      <button @click="pauseTimer" :disabled="!isRunning" class="control-button pause">
        Pausar
      </button>
      <button @click="resetTimer" class="control-button reset">
        Reiniciar
      </button>
    </div>
    <div class="pomodoro-info">
      <h3>Como funciona:</h3>
      <ul>
        <li>25 minutos de trabalho focado</li>
        <li>5 minutos de pausa</li>
        <li>Repita o ciclo 4 vezes</li>
        <li>Após 4 ciclos, faça uma pausa maior (15-30 minutos)</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.pomodoro-container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 20px;
}

.timer-display {
  font-size: 4rem;
  text-align: center;
  font-family: monospace;
  margin: 20px 0;
  color: #42b883;
}

.timer-display.break-time {
  color: #ff6b6b;
}

.timer-status {
  text-align: center;
  font-size: 1.2rem;
  margin-bottom: 20px;
  color: #666;
}

.controls {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 30px;
}

.control-button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: all 0.3s;
}

.control-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.start {
  background-color: #42b883;
  color: white;
}

.start:hover:not(:disabled) {
  background-color: #3aa876;
}

.pause {
  background-color: #ffc107;
  color: white;
}

.pause:hover:not(:disabled) {
  background-color: #e0a800;
}

.reset {
  background-color: #dc3545;
  color: white;
}

.reset:hover {
  background-color: #c82333;
}

.pomodoro-info {
  background-color: white;
  padding: 15px;
  border-radius: 4px;
  margin-top: 20px;
}

.pomodoro-info h3 {
  color: #2c3e50;
  margin-bottom: 10px;
}

.pomodoro-info ul {
  list-style-type: none;
  padding: 0;
}

.pomodoro-info li {
  margin-bottom: 8px;
  color: #666;
}
</style> 