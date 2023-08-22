<!-- src/components/ActionButton.vue -->
<template>
  <button class="action-button">{{ label }}</button>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export default defineComponent({
  props: {
    label: String,
  },
});
</script>

<style lang="scss" scoped>
.action-button {
  // Add your styling here
}
</style>
