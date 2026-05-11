<template>
  <div class="grid" :style="gridStyle">
    <div
      v-for="(tile, index) in tiles"
      :key="index"
      class="tile"
      :class="{ empty: tile === null }"
      @click="moveTile(index)"
    >
      {{ tile }}
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// Props
const props = defineProps({
  size: { type: Number, default: 4 } // default 4x4
})

// ✅ Define emits
const emit = defineEmits(['tileMoved'])

// Tiles state
const tiles = ref(generatePuzzle(props.size))

// Generate puzzle
function generatePuzzle(size) {
  const arr = Array.from({ length: size * size - 1 }, (_, i) => i + 1)
  arr.push(null) // empty space
  return shuffle(arr)
}

// Shuffle tiles
function shuffle(arr) {
  return arr.sort(() => Math.random() - 0.5)
}

// Move tile
function moveTile(index) {
  const emptyIndex = tiles.value.indexOf(null)
  const validMoves = getValidMoves(emptyIndex, props.size)

  if (validMoves.includes(index)) {
    [tiles.value[emptyIndex], tiles.value[index]] =
      [tiles.value[index], tiles.value[emptyIndex]]

    // ✅ Emit event to parent
    emit('tileMoved')
  }
}

// Valid moves
function getValidMoves(emptyIndex, size) {
  const moves = []
  const row = Math.floor(emptyIndex / size)
  const col = emptyIndex % size

  if (row > 0) moves.push(emptyIndex - size) // up
  if (row < size - 1) moves.push(emptyIndex + size) // down
  if (col > 0) moves.push(emptyIndex - 1) // left
  if (col < size - 1) moves.push(emptyIndex + 1) // right

  return moves
}

// Grid style
const gridStyle = computed(() => ({
  display: 'grid',
  gridTemplateColumns: `repeat(${props.size}, 80px)`,
  gap: '5px'
}))
</script>

<style scoped>
.tile {
  width: 80px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #000000;
  color: #fafafa;
  font-size: 20px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
}
.tile.empty {
  background: transparent;
  cursor: default;
}
</style>
