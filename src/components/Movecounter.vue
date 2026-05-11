<template>
  <div class="move-counter">
    🎯 Moves: {{ moves }}
  </div>
</template>

<script setup>
import { ref } from 'vue'

// reactive state
const moves = ref(0)

// increment function (called when a tile moves)
function increment() {
  moves.value++
}

// reset function (called when restarting the puzzle)
function reset() {
  moves.value = 0
}

// expose functions so parent can call them
defineExpose({ increment, reset })
</script>

<style scoped>
.move-counter {
  font-size: 18px;
  font-weight: bold;
  color: #444;
  margin: 10px 0;
}
</style>
