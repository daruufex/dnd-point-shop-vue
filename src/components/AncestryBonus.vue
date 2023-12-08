<script setup>
defineProps(['ancestryBonus'])

function handleInput(event) {
  const newValue = event.target.value;
  
  if (!isNaN(newValue) || newValue === '') {
    $emit('change', newValue === '' ? 0 : Number(newValue));
  }
}
</script>

<template>
  <td class="p-3 text-center">
    +&nbsp;
    <input
      class="bg-emerald-950 p-2 rounded w-10 text-center"
      type="text"
      :value="ancestryBonus"
      @input="handleInput"
    />
  </td>
</template>
