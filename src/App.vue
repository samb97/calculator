<script setup lang="ts">
import Calculator from './components/Calculator.vue'
</script>

<template>
  <div>
    <h1 class="text-6xl font-bold">The Calculator</h1>
    <Calculator :decimal-point-cap="4" />
  </div>
</template>
