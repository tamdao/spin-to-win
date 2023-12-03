<script setup lang="ts">
import Leaderboard from './components/Leaderboard.vue'
import SpinWheel from './components/SpinWheel.vue'
</script>

<template>
  <div>
    <p class="p-4 mt-9 text-center">
      <strong>Feeling lucky? </strong>Try out our spin and win game to win one
      of our exciting prizes.
    </p>
    <SpinWheel />
  </div>
  <div class="flex-1 max-h-[40%] md:max-h-[100%] md:w-[560px]">
    <Leaderboard />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
