<template>
  <button @click="startTimer">Start</button>
</template>

<script>
export default {
  methods: {
    startTimer() {
      this.$emit('start');
    },
  },
};
</script>
