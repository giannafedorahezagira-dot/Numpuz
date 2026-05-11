<template>
  <div id="app">
    <HomePage v-if="!gameStarted" @startGame="startGame" />

    <div v-else>
      <h1>🧩 Numpuz – Level {{ gridSize }}</h1>
      <Timer ref="timerRef" />
      <MoveCounter ref="moveCounterRef" />

      <div class="grid-wrapper">
        <PuzzleGrid
          :size="gridSize"
          @tileMoved="handleTileMoved"
        />
      </div>

      <button @click="restartGame">Restart Game</button>
      <button @click="exitToHome">Back to Home</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import HomePage from './components/HomePage.vue'
import PuzzleGrid from './components/PuzzleGrid.vue'
import Timer from './components/Timer.vue'
import MoveCounter from './components/MoveCounter.vue'

const gameStarted = ref(false)
const gridSize = ref(3) // default Level 1
const timerRef = ref(null)
const moveCounterRef = ref(null)

function startGame(size) {
  gridSize.value = size
  gameStarted.value = true
  timerRef.value?.resetTimer()
  moveCounterRef.value?.reset()
}

function handleTileMoved() {
  moveCounterRef.value.increment()
}

function restartGame() {
  timerRef.value.resetTimer()
  moveCounterRef.value.reset()
}

function exitToHome() {
  gameStarted.value = false
}
</script>

<style>
#app {
  text-align: center;
  font-family: Arial, sans-serif;
  margin-top: 20px;
}
.grid-wrapper {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
button {
  margin: 10px;
  padding: 8px 12px;
  border: none;
  border-radius: 6px;
  background: #4a90e2;
  color: white;
  cursor: pointer;
}
button:hover {
  background: #357ab8;
}
</style>
