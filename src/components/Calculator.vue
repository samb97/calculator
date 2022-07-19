
<script setup lang="ts">
import { computed, ref } from 'vue'

enum Operand {
  Plus = '+',
  Minus = '-',
  Divide = '-',
  Multiply = '-',
}

const numbers = [7, 8, 9, 4, 5, 6, 1, 2, 3, 0]
const numberSelection = ref<string>('')
const numberOne = ref<number | null>(null)
const numberTwo = ref<number | null>(null)
const operand = ref<Operand | null>(null)
const preText = computed(() => {
  return `${numberOne.value ?? ''} ${operand.value ?? ''} ${numberTwo.value ?? ''}`
})

function pushNumber(number: number) {
  numberSelection.value += number
}
</script>

<template>
  <div>
    <!-- Number pre-text -->
    <div>
      <input
        type="text"
        readonly
        aria-readonly
        :value="preText"
      />
    </div>

    <!-- Number input -->
    <div>
      <input
        type="text"
        readonly
        aria-readonly
        v-model="numberSelection"
      />
    </div>

    <!-- Number grid -->
    <div class="grid grid-cols-3 ">
      <button
        v-for="number in numbers"
        :key="`number-grid--number-${number}`"

        type="button"
        class="number-grid-item"

        @click="pushNumber(number)"
      >
        {{ number }}
      </button>
    </div>
  </div>  
</template>

<style lang="postcss" scoped>
input {
  @apply
    bg-white
    text-black
  ;
}

.number-grid-item {
  @apply
    cursor-pointer

    p-2

    text-xl
    text-center
    font-bold

    bg-slate-700

    hover:bg-slate-500
  ;
}
</style>
