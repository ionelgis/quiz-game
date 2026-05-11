<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-br from-indigo-950 via-purple-950 to-slate-900 px-4">
    <div class="bg-white/10 backdrop-blur-sm border border-white/20 rounded-3xl p-10 max-w-md w-full text-center shadow-2xl">
      <div class="text-6xl mb-4">{{ emoji }}</div>
      <h2 class="text-3xl font-bold text-white mb-1">{{ title }}</h2>
      <p class="text-purple-200 mb-6">{{ subtitle }}</p>

      <!-- Score circle -->
      <div class="relative inline-flex items-center justify-center mb-8">
        <svg class="w-36 h-36 -rotate-90" viewBox="0 0 120 120">
          <circle cx="60" cy="60" r="50" fill="none" stroke="rgba(255,255,255,0.1)" stroke-width="10" />
          <circle
            cx="60" cy="60" r="50" fill="none"
            :stroke="scoreColor"
            stroke-width="10"
            stroke-linecap="round"
            :stroke-dasharray="circumference"
            :stroke-dashoffset="dashOffset"
            class="transition-all duration-1000 ease-out"
          />
        </svg>
        <div class="absolute flex flex-col items-center">
          <span class="text-4xl font-bold text-white">{{ score }}</span>
          <span class="text-purple-300 text-sm">/ {{ total }}</span>
        </div>
      </div>

      <!-- Percentage -->
      <div class="mb-8">
        <div class="text-5xl font-bold mb-1" :class="scoreTextColor">{{ percentage }}%</div>
        <div class="text-purple-300 text-sm">Correct answers</div>
      </div>

      <!-- Stats -->
      <div class="grid grid-cols-2 gap-3 mb-8">
        <div class="bg-emerald-500/10 border border-emerald-500/30 rounded-xl p-3">
          <div class="text-2xl font-bold text-emerald-400">{{ score }}</div>
          <div class="text-emerald-200/70 text-sm">Correct</div>
        </div>
        <div class="bg-red-500/10 border border-red-500/30 rounded-xl p-3">
          <div class="text-2xl font-bold text-red-400">{{ total - score }}</div>
          <div class="text-red-200/70 text-sm">Incorrect</div>
        </div>
      </div>

      <button
        @click="$emit('restart')"
        class="w-full bg-purple-600 hover:bg-purple-500 active:bg-purple-700 text-white font-bold py-4 px-8 rounded-2xl text-lg transition-all duration-200 shadow-lg hover:shadow-purple-500/30 hover:-translate-y-0.5"
      >
        Play Again
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  score: Number,
  total: Number,
})

defineEmits(['restart'])

const percentage = computed(() => Math.round((props.score / props.total) * 100))

const circumference = 2 * Math.PI * 50
const dashOffset = computed(() => circumference - (percentage.value / 100) * circumference)

const emoji = computed(() => {
  if (percentage.value >= 90) return '🏆'
  if (percentage.value >= 70) return '🎉'
  if (percentage.value >= 50) return '😊'
  return '📚'
})

const title = computed(() => {
  if (percentage.value >= 90) return 'Outstanding!'
  if (percentage.value >= 70) return 'Great Job!'
  if (percentage.value >= 50) return 'Not Bad!'
  return 'Keep Learning!'
})

const subtitle = computed(() => {
  if (percentage.value >= 90) return "You're a genius — perfect score territory!"
  if (percentage.value >= 70) return 'You really know your stuff!'
  if (percentage.value >= 50) return 'You passed — room to improve though!'
  return 'Practice makes perfect. Try again!'
})

const scoreColor = computed(() => {
  if (percentage.value >= 70) return '#34d399'
  if (percentage.value >= 50) return '#fbbf24'
  return '#f87171'
})

const scoreTextColor = computed(() => {
  if (percentage.value >= 70) return 'text-emerald-400'
  if (percentage.value >= 50) return 'text-amber-400'
  return 'text-red-400'
})
</script>
