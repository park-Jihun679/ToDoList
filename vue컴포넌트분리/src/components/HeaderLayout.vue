<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <header class="header">
    <h1>{{ title }}</h1>
  </header>
</template>

<style scoped>
/* header */
.header {
  padding: 1rem;
  font-size: 1.5rem;
  text-align: center;
  color: white;
  background: rgba(237, 193, 211);
  background: linear-gradient(
    166deg,
    rgba(237, 193, 211, 1) 0%,
    rgba(219, 192, 216, 1) 35%,
    rgba(127, 188, 242, 1) 100%
  );
  border-radius: 20px 20px 0 0;
}
</style>
