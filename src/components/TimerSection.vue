<script lang="ts" setup>
import { ref, onUnmounted, watch } from 'vue'

const props = defineProps({
  showResult: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['time'])

const time = ref(0)
let intervalId: any

const startTimer = () => {
  intervalId = setInterval(() => {
    time.value++
  }, 1000)
}

const stopTimer = () => {
  clearInterval(intervalId)
}

const resetTimer = () => {
  time.value = 0
}

const formattedTime = () => {
  const minutes = Math.floor(time.value / 60)
  const seconds = time.value % 60
  return `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`
}

// Start the timer when the component is created
startTimer()

// Stop the timer when the component is about to be unmounted
onUnmounted(() => {
  stopTimer()
})

watch(
  () => props.showResult,
  (newValue) => {
    if (newValue) {
      // Do something when showResult becomes true, e.g., stop the timer
      stopTimer()
      emit('time', time)
    }
  }
)
</script>

<template>
  <div>
    <h1 class="text-3xl">Timer: {{ formattedTime() }}</h1>
    <button @click="stopTimer()">stop</button>
  </div>
</template>

<style scoped>
/* Your styles go here */
</style>
