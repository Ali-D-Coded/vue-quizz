<script setup lang="ts">
import { ref, watch } from 'vue'
import { quizzes as q } from '../data/quizzes'
import QuizCard from '@/components/QuizCard.vue'

const quizzes = ref(q)
const search = ref('')

watch(search, () => {
  quizzes.value = q.filter((it) => it.name.toLowerCase().includes(search.value.toLowerCase()))
})
</script>

<template>
  <div class="max-w-[1000px] mx-auto bg-slate-50">
    <header class="flex flex-col sm:flex-row p-5 gap-10 box-border">
      <h1 class="text-3xl font-black text-green-600 bg-yellow-400 p-2 -skew-x-12 rounded">
        Quizzes
      </h1>
      <input v-model.trim="search" type="text" placeholder="Search..." class="p-2 outline-none" />
    </header>
    <main class="flex flex-wrap gap-3 p-2 justify-center">
      <QuizCard v-for="quiz in quizzes" :key="quiz.id" :quiz="quiz" />
    </main>
  </div>
</template>
