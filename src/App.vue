<template>
  <StartScreen v-if="phase === 'start'" @start="startQuiz" />
  <QuestionCard
    v-else-if="phase === 'quiz'"
    :key="currentIndex"
    :question="questions[currentIndex]"
    :current="currentIndex"
    :total="questions.length"
    :score="score"
    @answer="handleAnswer"
    @next="nextQuestion"
  />
  <ResultsScreen
    v-else-if="phase === 'results'"
    :score="score"
    :total="questions.length"
    @restart="restart"
  />
</template>

<script setup>
import { ref } from 'vue'
import { questions } from './data/questions.js'
import StartScreen from './components/StartScreen.vue'
import QuestionCard from './components/QuestionCard.vue'
import ResultsScreen from './components/ResultsScreen.vue'

const phase = ref('start')
const currentIndex = ref(0)
const score = ref(0)

function startQuiz() {
  currentIndex.value = 0
  score.value = 0
  phase.value = 'quiz'
}

function handleAnswer(correct) {
  if (correct) score.value++
}

function nextQuestion() {
  if (currentIndex.value + 1 < questions.length) {
    currentIndex.value++
  } else {
    phase.value = 'results'
  }
}

function restart() {
  phase.value = 'start'
}
</script>
