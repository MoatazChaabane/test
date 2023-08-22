<!-- src/components/TimerDisplay.vue -->
<template>
  <div class="timer-display">
    <p>Current Period: {{ currentPeriod }}</p>
    <p>Total Period: {{ totalPeriod }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  props: {
    currentPeriod: String,
    totalPeriod: String,
  },
});
</script>

<style lang="scss" scoped>
.timer-display {
  // Add your styling here
}
</style>
