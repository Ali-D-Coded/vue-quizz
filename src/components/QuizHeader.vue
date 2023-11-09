<script setup lang="ts">
const { questionStatus, barpercentage } = defineProps(['questionStatus', 'barpercentage'])
</script>
<template>
  <div class="grid gap-2">
    <p class="text-3xl">Questions {{ questionStatus }}</p>
    <div class="w-[300px] h-[40px] border border-amber-300">
      <div
        class="border border-amber-400 h-full flex-1 bg-amber-200"
        :style="{
          width: barpercentage
        }"
      ></div>
    </div>
  </div>
</template>

<style scoped></style>
