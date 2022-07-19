<script setup lang="ts">
import Calculator from './components/Calculator.vue'
</script>

<template>
  <div class="container mx-auto px-2">
    <h1 class="text-6xl font-bold mb-4">The Calculator</h1>
    <Calculator
      :decimal-point-cap="4"
      class="max-w-xl"
    />
  </div>
</template>
