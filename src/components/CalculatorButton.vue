<template>
  <button
    type="button"
    class="button"
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
</style>
