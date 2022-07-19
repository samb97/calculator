
<script setup lang="ts">
import { computed, ref } from 'vue'
import CalculatorButton from './CalculatorButton.vue'

interface Props {
  decimalPointCap?: number
}

const { decimalPointCap = 2 } = defineProps<Props>()

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

function prepareNumber(num: (number | string)) {
  return Number(Number(num).toFixed(decimalPointCap))
}

function calculateAnswer(): number {
  if (numberOne.value === null) {
    return 0
  }

  if (numberTwo.value === null) {
    return 0
  }

  if (operand.value === Operand.Plus) {
    return numberOne.value + numberTwo.value
  }

  if (operand.value === Operand.Minus) {
    return numberOne.value - numberTwo.value
  }

  if (operand.value === Operand.Divide) {
    return numberOne.value / numberTwo.value
  }

  if (operand.value === Operand.Multiply) {
    return numberOne.value * numberTwo.value
  }

  return 0
}

function resetNumberSelection() {
  numberSelection.value = ''
}

function pushNumber(number: number) {
  numberSelection.value += number
}

function setOperand(_operand: Operand) {
  if (numberSelection.value === '') {
    return
  }

  if (numberOne.value === null) {
    numberOne.value = prepareNumber(numberSelection.value)
    resetNumberSelection()
  } else if (numberTwo.value === null) {
    numberTwo.value = prepareNumber(numberSelection.value)
    resetNumberSelection()
  }

  if (numberOne.value !== null && numberTwo.value !== null) {
    numberOne.value = prepareNumber(calculateAnswer())
    numberTwo.value = null
  }

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
