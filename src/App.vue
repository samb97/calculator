<script setup lang="ts">
import Calculator from './components/Calculator.vue'
</script>

<template>
  <div class="container mx-auto px-2 text-center">
    <div class="py-12">
      <h1 class="text-6xl font-bold mb-4">The Calculator</h1>
      <p>A basic number calculator built using Vue3 + TypeScript & TailwindCSS.</p>
    </div>
    <Calculator
      :decimal-point-cap="4"
      class="max-w-md mx-auto"
    />
  </div>
</template>
