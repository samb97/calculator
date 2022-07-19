
<script setup lang="ts">
import { computed, ref } from 'vue'
import CalculatorButton from './CalculatorButton.vue'

enum Operand {
  Plus = '+',
  Minus = '-',
  Divide = '/',
  Multiply = '*',
}

const operands = [
  Operand.Plus,
  Operand.Minus,
  Operand.Divide,
  Operand.Multiply,
]
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

function setOperand(_operand: Operand) {
  operand.value = _operand
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

    <div class="grid grid-cols-4">

      <!-- Number grid -->
      <div class="col-span-3 grid grid-cols-3 ">
        <CalculatorButton
          v-for="number in numbers"
          :key="`button-grid--number-${number}`"

          @click="pushNumber(number)"
        >
          {{ number }}
        </CalculatorButton>
      </div>

      <!-- Operands -->
      <div class="grid grid-cols-1">
        <CalculatorButton
          v-for="operand in operands"
          :key="`button-grid--operand-${operand}`"

          @click="setOperand(operand)"
        >
          {{ operand }}
        </CalculatorButton>
      </div>
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
</style>
