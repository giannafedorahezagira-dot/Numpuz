<template>
  <div class="home-page">
    <h1>🧩 Welcome to Numpuz</h1>
    <p class="subtitle">Choose your challenge level:</p>

    <div class="levels">
      <button @click="$emit('startGame', 3)">Level 1 – Easy (3x3)</button>
      <button @click="$emit('startGame', 4)">Level 2 – Medium (4x4)</button>
      <button @click="$emit('startGame', 5)">Level 3 – Hard (5x5)</button>
      <button @click="$emit('startGame', 6)">Level 4 – Expert (6x6)</button>
    </div>
  </div>
</template>

<script setup>
// Emits the chosen level back to App.vue
</script>

<style scoped>
.home-page {
  text-align: center;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: #fff;
  padding: 40px;
}

/* Title */
h1 {
  font-size: 3rem;
  margin-bottom: 10px;
  text-shadow: 2px 2px 8px rgba(0,0,0,0.4);
}

/* Subtitle */
.subtitle {
  font-size: 1.2rem;
  margin-bottom: 30px;
  opacity: 0.9;
}

/* Level buttons */
.levels {
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-width: 300px;
  margin: 0 auto;
}

button {
  padding: 14px 20px;
  border: none;
  border-radius: 30px;
  background: linear-gradient(45deg, #ff9a9e, #fad0c4);
  color: #333;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0,0,0,0.25);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 16px rgba(0,0,0,0.35);
  background: linear-gradient(45deg, #a18cd1, #fbc2eb);
}
</style>
