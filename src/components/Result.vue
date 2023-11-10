<script setup lang="ts">
const { result } = defineProps(['result'])
console.log({ result })
</script>
<template>
  <div class="text-center text-4xl">
    You scored
    <b>
      {{ result }}
    </b>
  </div>
</template>

<style scoped></style>
