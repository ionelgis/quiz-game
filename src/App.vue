<template>
  <StartScreen v-if="phase === 'start'" @start="startQuiz" />
  <QuestionCard
    v-else-if="phase === 'quiz'"
    :key="currentIndex"
    :question="activeQuestions[currentIndex]"
    :current="currentIndex"
    :total="activeQuestions.length"
    :score="score"
    @answer="handleAnswer"
    @next="nextQuestion"
  />
  <ResultsScreen
    v-else-if="phase === 'results'"
    :score="score"
    :total="activeQuestions.length"
    @restart="restart"
  />
</template>

<script setup>
import { ref, computed } from 'vue'
import { questions, historyQuestions } from './data/questions.js'
import StartScreen from './components/StartScreen.vue'
import QuestionCard from './components/QuestionCard.vue'
import ResultsScreen from './components/ResultsScreen.vue'

const phase = ref('start')
const currentIndex = ref(0)
const score = ref(0)
const quizType = ref('general')

const activeQuestions = computed(() =>
  quizType.value === 'history' ? historyQuestions : questions
)

function startQuiz(type) {
  quizType.value = type
  currentIndex.value = 0
  score.value = 0
  phase.value = 'quiz'
}

function handleAnswer(correct) {
  if (correct) score.value++
}

function nextQuestion() {
  if (currentIndex.value + 1 < activeQuestions.value.length) {
    currentIndex.value++
  } else {
    phase.value = 'results'
  }
}

function restart() {
  phase.value = 'start'
}
</script>
