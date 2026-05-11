<template>
  <div id="app">
    <h1>🧩 Numpuz – Level 1</h1>

    <!-- Timer -->
    <Timer ref="timerRef" />

    <!-- Move Counter -->
    <MoveCounter ref="moveCounterRef" />

    <!-- Puzzle Grid (Level 1 = 3x3) -->
    <div class="grid-wrapper">
      <PuzzleGrid
        :size="3"
        @tileMoved="handleTileMoved"
        @restart="restartGame"
      />
    </div>

    <!-- Restart Button -->
    <button @click="restartGame">Restart Game</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import PuzzleGrid from './components/PuzzleGrid.vue'
import Timer from './components/Timer.vue'
import MoveCounter from './components/MoveCounter.vue'

const timerRef = ref(null)
const moveCounterRef = ref(null)

function handleTileMoved() {
  moveCounterRef.value.increment()
}

function restartGame() {
  timerRef.value.resetTimer()
  moveCounterRef.value.reset()
}
</script>

<style>
#app {
  text-align: center;
  font-family: Arial, sans-serif;
  margin-top: 20px;
}

/* Center the puzzle grid */
.grid-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

button {
  margin-top: 15px;
  padding: 8px 12px;
  border: none;
  border-radius: 6px;
  background: #000000;
  color: white;
  cursor: pointer;
}
</style>
