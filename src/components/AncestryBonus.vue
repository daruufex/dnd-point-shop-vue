<script setup>
import { defineProps } from 'vue';

const props = defineProps(['value']);

const handleInput = (newValue) => {
  if (isNaN(Number(newValue))) {
    $emit('updateAncestryBonus', 0);
    return;
  }
  if (newValue.length > 1) {
    $emit('updateAncestryBonus', newValue.slice(0, 1));
    return;
  }
  $emit('updateAncestryBonus', newValue);
};

const handleFocusOut = (event) => {
  if (event.target.value === '') $emit('updateAncestryBonus', 0);
};
</script>

<template>
  <td class="p-3 text-center">
    +&nbsp;
    <input
      class="bg-emerald-950 p-2 rounded w-10 text-center"
      type="text"
      :value="value"
      @input="handleInput"
      @focusout="handleFocusOut"
    />
  </td>
</template>
