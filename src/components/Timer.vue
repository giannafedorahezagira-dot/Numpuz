<template>
  <div class="timer">
    ⏱️ Time: {{ formattedTime }}
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

// reactive state
const time = ref(0)
let intervalId = null

// start timer when mounted
onMounted(() => {
  intervalId = setInterval(() => {
    time.value++
  }, 1000)
})

// clear timer when component unmounts
onUnmounted(() => {
  clearInterval(intervalId)
})

// format time as mm:ss
const formattedTime = computed(() => {
  const minutes = Math.floor(time.value / 60)
  const seconds = time.value % 60
  return `${minutes}:${seconds.toString().padStart(2, '0')}`
})

// expose reset function to parent
function resetTimer() {
  time.value = 0
}
defineExpose({ resetTimer })
</script>

<style scoped>
.timer {
  font-size: 18px;
  font-weight: bold;
  color: #333;
  margin: 10px 0;
}
</style>
