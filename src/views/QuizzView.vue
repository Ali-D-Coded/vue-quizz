<script setup lang="ts">
import QuizHeader from '@/components/QuizHeader.vue'
import Questions from '@/components/Questions.vue'
import Result from '@/components/Result.vue'
import { quizzes } from '@/data/quizzes'
import { useRoute } from 'vue-router'
import { computed, ref, watch } from 'vue'

const route = useRoute()
const quizid: number = parseInt(route.params.quizId)
const quiz = quizzes.find((q) => q.id == quizid)
const currentQuestionIndex = ref(0)
const showResult = ref(false)
// console.log(quiz?.questions[currentQuestionIndex.value])

const questionStatus = computed(() => `${currentQuestionIndex.value + 1}/${quiz?.questions.length}`)
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
  if (!exists) {
    numberOfCorrectAnswers.value.push(value)
  }
  if (quiz?.questions?.length - 1 === currentQuestionIndex.value) {
    showResult.value = true
  }
}
</script>

<template>
  <div class="max-w-[1000px] mx-auto bg-slate-50">
    {{ numberOfCorrectAnswers }}
    <header class="p-10">
      <QuizHeader :barpercentage="barPercentage" :questionStatus="questionStatus" />
    </header>
    <main class="p-10">
      <Questions
        v-if="!showResult"
        :question="quiz?.questions[currentQuestionIndex]"
        @isCorrect="updateAnswer"
        @updateIndex="currentQuestionIndex++"
      />
      <Result v-else />
    </main>
  </div>
</template>

<style></style>
