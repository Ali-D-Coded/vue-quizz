<script setup lang="ts">
const { question } = defineProps(['question'])

const emit = defineEmits(['selectedOption'])

function validateAnswer(question: any) {
  // if (question.isCorrect) {
  emit('selectedOption', question)
  // }
}
</script>
<template>
  <div>
    <h2 class="text-4xl">
      {{ question.text }}
    </h2>

    <section class="grid gap-2">
      <div
        v-for="q of question.options"
        :key="q.id"
        @click="() => validateAnswer(q)"
        class="bg-slate-200 w-full flex items-center gap-5 text-xl"
      >
        <div class="w-fit p-3 bg-amber-300">{{ q?.label }}</div>
        <div>{{ q?.text }}</div>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
