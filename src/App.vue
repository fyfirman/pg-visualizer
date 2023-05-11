<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <RouterView />
</template>

<style lang="scss">
  main {
    width: 100%;

    & > .plan-container {
      height: 100vh;
    }
  }
</style>
