<template>
  <div class="app">
    <h1>Time Tracker App</h1>
    <TimerDisplay :currentPeriod="currentPeriod" :totalPeriod="totalPeriod" />
    <ActionButton label="Start" />
    <ActionButton label="Stop" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import TimerDisplay from "@/components/TimerDisplay.vue";
import ActionButton from "@/components/ActionButton.vue";

export default defineComponent({
  components: {
    TimerDisplay,
    ActionButton,
  },
  setup() {
    const currentPeriod = ref("00:bara:00");
    const totalPeriod = ref("00:00:00");

    return { currentPeriod, totalPeriod };
  },
});
</script>

<style lang="scss">
.app {
  // Add your styling here
}
</style>
