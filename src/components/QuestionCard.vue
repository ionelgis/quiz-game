<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-br from-indigo-950 via-purple-950 to-slate-900 px-4 py-8">
    <div class="w-full max-w-2xl">

      <!-- Progress bar -->
      <div class="mb-6">
        <div class="flex justify-between text-purple-200 text-sm mb-2">
          <span>Question {{ current + 1 }} of {{ total }}</span>
          <span class="bg-purple-700/50 px-3 py-0.5 rounded-full text-purple-200 text-xs font-medium">
            {{ question.category }}
          </span>
        </div>
        <div class="h-2 bg-white/10 rounded-full overflow-hidden">
          <div
            class="h-full bg-purple-500 rounded-full transition-all duration-500"
            :style="{ width: `${((current + 1) / total) * 100}%` }"
          />
        </div>
      </div>

      <!-- Score badge -->
      <div class="flex justify-end mb-4">
        <div class="bg-white/10 border border-white/20 rounded-xl px-4 py-2 text-white text-sm font-semibold">
          Score: <span class="text-purple-300">{{ score }}</span>
        </div>
      </div>

      <!-- Question -->
      <div class="bg-white/10 backdrop-blur-sm border border-white/20 rounded-3xl p-8 mb-5 shadow-2xl">
        <h2 class="text-white text-xl font-semibold leading-relaxed">{{ question.question }}</h2>
      </div>

      <!-- Options -->
      <div class="grid grid-cols-1 gap-3">
        <button
          v-for="(option, index) in question.options"
          :key="option"
          :disabled="answered"
          @click="select(option)"
          :class="optionClass(option, index)"
          class="w-full text-left px-6 py-4 rounded-2xl font-medium text-base transition-all duration-200 border-2 flex items-center gap-4"
        >
          <span class="w-8 h-8 rounded-full flex items-center justify-center font-bold text-sm shrink-0"
            :class="labelClass(option)">
            {{ letters[index] }}
          </span>
          {{ option }}
        </button>
      </div>

      <!-- Next / Finish button -->
      <div v-if="answered" class="mt-6 flex justify-end">
        <button
          @click="$emit('next')"
          class="bg-purple-600 hover:bg-purple-500 active:bg-purple-700 text-white font-bold py-3 px-8 rounded-2xl transition-all duration-200 shadow-lg hover:shadow-purple-500/30 hover:-translate-y-0.5"
        >
          {{ current + 1 < total ? 'Next Question →' : 'See Results' }}
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  question: Object,
  current: Number,
  total: Number,
  score: Number,
})

const emit = defineEmits(['answer', 'next'])

const letters = ['A', 'B', 'C', 'D']
const selected = ref(null)
const answered = ref(false)

function select(option) {
  if (answered.value) return
  selected.value = option
  answered.value = true
  emit('answer', option === props.question.answer)
}

function optionClass(option, index) {
  if (!answered.value) {
    return 'bg-white/10 border-white/20 text-white hover:bg-white/20 hover:border-purple-400 cursor-pointer'
  }
  if (option === props.question.answer) {
    return 'bg-emerald-500/20 border-emerald-400 text-emerald-200 cursor-default'
  }
  if (option === selected.value) {
    return 'bg-red-500/20 border-red-400 text-red-200 cursor-default'
  }
  return 'bg-white/5 border-white/10 text-white/40 cursor-default'
}

function labelClass(option) {
  if (!answered.value) return 'bg-white/20 text-white'
  if (option === props.question.answer) return 'bg-emerald-500 text-white'
  if (option === selected.value) return 'bg-red-500 text-white'
  return 'bg-white/10 text-white/40'
}
</script>
