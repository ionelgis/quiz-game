<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-br from-indigo-950 via-purple-950 to-slate-900 px-4">
    <div class="bg-white/10 backdrop-blur-sm border border-white/20 rounded-3xl p-10 max-w-md w-full text-center shadow-2xl">
      <div class="text-6xl mb-4">🧠</div>
      <h1 class="text-4xl font-bold text-white mb-2">Quiz Game</h1>
      <p class="text-purple-200 mb-8 text-lg">Pick a quiz and test your knowledge!</p>

      <div class="flex flex-col gap-4">
        <button
          @click="$emit('start', 'general')"
          class="w-full bg-purple-600 hover:bg-purple-500 active:bg-purple-700 text-white font-bold py-4 px-8 rounded-2xl text-lg transition-all duration-200 shadow-lg hover:shadow-purple-500/30 hover:-translate-y-0.5 flex items-center justify-center gap-3"
        >
          <span>🌍</span> General Quiz
          <span class="ml-auto text-purple-300 text-sm font-normal">10 questions · 6 categories</span>
        </button>

        <button
          @click="$emit('start', 'history')"
          class="w-full bg-amber-600 hover:bg-amber-500 active:bg-amber-700 text-white font-bold py-4 px-8 rounded-2xl text-lg transition-all duration-200 shadow-lg hover:shadow-amber-500/30 hover:-translate-y-0.5 flex items-center justify-center gap-3"
        >
          <span>📜</span> History Quiz
          <span class="ml-auto text-amber-200 text-sm font-normal">10 questions · History</span>
        </button>

        <button
          @click="$emit('start', 'math')"
          class="w-full bg-emerald-600 hover:bg-emerald-500 active:bg-emerald-700 text-white font-bold py-4 px-8 rounded-2xl text-lg transition-all duration-200 shadow-lg hover:shadow-emerald-500/30 hover:-translate-y-0.5 flex items-center justify-center gap-3"
        >
          <span>🔢</span> Math Quiz
          <span class="ml-auto text-emerald-200 text-sm font-normal">10 questions · Math</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineEmits(['start'])
</script>
