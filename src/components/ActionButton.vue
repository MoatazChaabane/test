<template>
  <button class="action-button" @click="handleClick">{{ label }}</button>
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from "vue";

export default defineComponent({
  props: {
    label: String,
    isRunning: Boolean, // Pass the isTimerRunning prop
  },
  setup(props, { emit }) {
    const handleClick = () => {
      emit("click");
    };

    return { handleClick };
  },
});
</script>

<style lang="scss" scoped>
.action-button {
  // Add your styling here
}
</style>
