<template>
  <div>
    <ul>
      <li v-for="time in times" :key="time.id">{{ time }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['times'],
};
</script>
