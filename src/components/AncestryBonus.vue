<script setup>
defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

/*
  Unfortunatelly, due to some strange behaviour, I had to update
  event.target.value manually. Vue seems to ignore the second and
  further keystrokes and doesn't exactly sync the value correctly.
*/
function handleInput(event) {
  let newValue = event.target.value

  if (isNaN(Number(newValue))) newValue = 0
  if (newValue.length > 1) newValue = newValue.slice(0, 1)

  emit('update:modelValue', newValue)
  event.target.value = newValue
}

function handleFocusOut(event) {
  if (event.target.value === '') emit('update:modelValue', 0)
}
</script>

<template>
  <td class="p-3 text-center">
    +&nbsp;
    <input
      class="bg-emerald-950 p-2 rounded w-10 text-center"
      type="text"
      :value="modelValue"
      @input="handleInput"
      @focusout="handleFocusOut"
    />
  </td>
</template>
