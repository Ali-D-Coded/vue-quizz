<script setup lang="ts">
import { useRouter } from 'vue-router'

const { result, timeTook } = defineProps(['result', 'timeTook'])

const router = useRouter()
</script>
<template>
  <div class="text-center text-4xl mb-5">
    You scored
    <b>
      {{ result }}
    </b>
    <br />
    and you took
    <b>
      {{ timeTook }}
    </b>
    seconds to complete
  </div>
  <button
    @click="router.push('/')"
    class="bg-green-400 text-2xl py-2 px-3 block rounded-md mx-auto w-fit"
  >
    Done
  </button>
</template>

<style scoped></style>
