<script setup>
defineProps(['disbled'])

const style =
  'w-7 mr-1 border rounded border-emerald-700 ' +
  'hover:bg-emerald-700 active:bg-emerald-950 transition-colors ' +
  'disabled:bg-emerald-950 disabled:text-gray-500'
</script>

<template>
  <button :class="style" @click="$emit('increaseScore')" :disabled="disabled">
    <slot></slot>
  </button>
</template>
