<template>
  <div>
    <p>{{ formattedTime }}</p>
  </div>
</template>

<script>
export default {
  props: ['time'],
  computed: {
    formattedTime() {
      const minutes = Math.floor(this.time / 60);
      const seconds = this.time % 60;
      return `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
    },
  },
};
</script>
