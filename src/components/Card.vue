<script setup lang="ts">
import { defineProps } from 'vue'

const { quiz } = defineProps(['quiz'])
</script>
<template>
  <div class="bg-slate-200 w-fit max-w-[300px] rounded-md">
    <img :src="quiz.img" alt="" class="h-[200px] w-[200px] rounded-t-md" />
    <div class="my-2 p-1">
      <h2 class="font-bold">{{ quiz.name }}</h2>
      <p>{{ quiz.questions.length }} questions</p>
    </div>
  </div>
</template>

<style scoped></style>
