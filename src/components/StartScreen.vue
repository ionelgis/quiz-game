<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-br from-indigo-950 via-purple-950 to-slate-900 px-4">
    <div class="bg-white/10 backdrop-blur-sm border border-white/20 rounded-3xl p-10 max-w-md w-full text-center shadow-2xl">
      <div class="text-6xl mb-4">🧠</div>
      <h1 class="text-4xl font-bold text-white mb-2">Quiz Game</h1>
      <p class="text-purple-200 mb-8 text-lg">Test your knowledge across 10 questions!</p>

      <div class="grid grid-cols-2 gap-3 mb-8 text-sm">
        <div class="bg-white/10 rounded-xl p-3">
          <div class="text-2xl font-bold text-white">10</div>
          <div class="text-purple-200">Questions</div>
        </div>
        <div class="bg-white/10 rounded-xl p-3">
          <div class="text-2xl font-bold text-white">6</div>
          <div class="text-purple-200">Categories</div>
        </div>
      </div>

      <button
        @click="$emit('start')"
        class="w-full bg-purple-600 hover:bg-purple-500 active:bg-purple-700 text-white font-bold py-4 px-8 rounded-2xl text-lg transition-all duration-200 shadow-lg hover:shadow-purple-500/30 hover:-translate-y-0.5"
      >
        Start Quiz
      </button>
    </div>
  </div>
</template>

<script setup>
defineEmits(['start'])
</script>
