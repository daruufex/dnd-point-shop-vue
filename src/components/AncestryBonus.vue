<script setup>
defineProps(['ancestryBonus'])
</script>

<template>
  <td class="p-3 text-center">
    +&nbsp;
    <input
      class="bg-emerald-950 p-2 rounded w-10 text-center"
      type="text"
      :value="ancestryBonus"
      @input="$emit('change', Number($event.target.value))"
    />
  </td>
</template>
