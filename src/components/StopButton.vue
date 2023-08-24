<template>
  <button @click="stopTimer">Stop</button>
</template>

<script>
export default {
  methods: {
    stopTimer() {
      this.$emit('stop');
    },
  },
};
</script>
