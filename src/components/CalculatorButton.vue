<script setup lang="ts">
interface Props {
  isImportant?: boolean
}

const { isImportant = false } = defineProps<Props>()
</script>

<template>
  <button
    type="button"
    class="button"
    :class="{'is-important': isImportant}"
  >
    <slot />
  </button>
</template>

<style lang="postcss" scoped>
.button {
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

.button.is-important {
  @apply
    bg-orange-700
    hover:bg-orange-500
  ;
}
</style>
