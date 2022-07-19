<script setup lang="ts">
import { ref } from '@vue/reactivity'
import Calculator from './components/Calculator.vue'

const decimalPointCap = ref(4)
</script>

<template>
  <div class="container mx-auto px-2 text-center">
    <div class="py-12 space-y-12">
      <div>
        <h1 class="text-6xl font-bold mb-4">The Calculator</h1>
        <p>A basic number calculator built using Vue3 + TypeScript & TailwindCSS.</p>
      </div>
      <div class="text-left p-4 max-w-md mx-auto border border-white rounded-lg">
        <p class="font-bold">Props:</p>
        <div class="flex items-center space-x-2">
          <p><code>decimalPointCap</code></p>
          <input
            type="number"
            v-model="decimalPointCap"
            min="0"
            max="6"
            class="text-black text-center"
          />
        </div>
      </div>
    </div>
    <Calculator
      :key="`using-decimal-point--${decimalPointCap}`"
      :decimal-point-cap="decimalPointCap"
      class="max-w-md mx-auto rounded-lg overflow-hidden bg-slate-600 border-2 border-white drop-shadow-md"
    />
  </div>
</template>
