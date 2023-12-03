<template>
  <div class="flex flex-col h-full min-w-[320px] overflow-hidden">
    <h2 class="text-2xl font-bold py-4 text-center">Leaderboard</h2>
    <ul class="overflow-auto h-full divide-y divide-gray-200 border">
      <li v-for="item in topUsers" class="bg-white hover:bg-gray-100">
        <div class="flex flex-row gap-4 items-center">
          <div class="p-2">
            <div class="w-8 h-8 rounded-full bg-yellow-500"></div>
          </div>
          <div class="text-sm flex-1 font-semibold">{{ item.name }}</div>
          <div class="bg-yellow-500 flex flex-col p-2 gap-1 font-semibold">
            <div class="text-xs text-right px-1 bg-white rounded-full">
              {{ item.win }} WINS
            </div>
            <div class="text-xs px-1 bg-white rounded-full">
              {{ item.minutes }} MINUTES
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const topUsers = ref([
  {
    name: 'User 1',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 2',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 3',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 4',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 5',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 6',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 7',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 8',
    win: 36,
    minutes: 9.36,
  },
  {
    name: 'User 9',
    win: 36,
    minutes: 9.36,
  },
])
</script>
