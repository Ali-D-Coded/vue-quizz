<script setup lang="ts">
import QuizHeader from '@/components/QuizHeader.vue'
import QuestionsSection from '@/components/QuestionsSection.vue'
import ResultSection from '@/components/ResultSection.vue'
import { quizzes } from '@/data/quizzes'
import { useRoute } from 'vue-router'
import { computed, ref } from 'vue'
import ConfettiExplosion from 'vue-confetti-explosion'
import TimerSection from '@/components/TimerSection.vue'

const route = useRoute()
const quizid: number = parseInt(route.params.quizId)
const quiz = quizzes.find((q) => q.id == quizid)
const currentQuestionIndex = ref(0)
const showResult = ref(false)
const timeTook = ref('0:00')
// console.log(quiz?.questions[currentQuestionIndex.value])

const questionStatus = computed(() => `${currentQuestionIndex.value}/${quiz?.questions.length}`)
const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz?.questions?.length) * 100}%`
)

const numberOfCorrectAnswers = ref([])

function updateAnswer(value: any) {
  console.log({ value })
  const exists = numberOfCorrectAnswers.value.find(
    (a) =>
      `${a.id}_${a.text}_${a.label}_${a.isCorrect}` ===
      `${value.id}_${value.text}_${value.label}_${value.isCorrect}`
  )
  if (!exists && value.isCorrect) {
    numberOfCorrectAnswers.value.push(value)
  }
  console.log(quiz?.questions?.length - 1, currentQuestionIndex.value)
  if (+quiz?.questions?.length - 1 === +currentQuestionIndex.value) {
    showResult.value = true
  }
  currentQuestionIndex.value++
}
</script>

<template>
  <div class="max-w-[1000px] mx-auto bg-slate-50">
    <ConfettiExplosion
      v-if="showResult"
      class="absolute top-0 left-[50%] w-full h-full"
      :particleCount="500"
      :force="0.3"
    />
    <header class="p-10 flex items-center justify-between">
      <QuizHeader :barpercentage="barPercentage" :questionStatus="questionStatus" />
      <TimerSection :showResult="showResult" @time="(v) => (timeTook = v.value)" />
    </header>
    <main class="p-10">
      <QuestionsSection
        v-if="!showResult"
        :question="quiz?.questions[currentQuestionIndex]"
        @selectedOption="updateAnswer"
      />
      <ResultSection
        v-else
        :result="`${numberOfCorrectAnswers.length}/${quiz?.questions.length}`"
        :time-took="timeTook"
      />
    </main>
  </div>
</template>

<style></style>
