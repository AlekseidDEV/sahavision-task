<script setup lang="ts">
defineProps<{
  colorBtn?: string
}>()
</script>

<template>
<button :class="colorBtn">
  <slot></slot>
</button>
</template>

<style scoped lang="scss">
  .green {
    background-color: #4eb988;
  }
</style>