<script setup>
import { ref, inject, computed } from 'vue'
import defaults from '../defaults'

import StatControls from './StatControls.vue'
import AncestryBonus from './AncestryBonus.vue'

defineProps(['name'])

const score = ref(10)
const ancestryBonus = ref(0)

const { points, setPoints } = inject('points')

const finalScore = computed(() => score.value + Number(ancestryBonus.value))
const modifier = computed(() => Math.floor((finalScore.value - 10) / 2))

function increaseScore() {
  setPoints(points.value - defaults.scoreCosts[score.value + 1])
  score.value++
}

function decreaseScore() {
  setPoints(points.value + defaults.scoreCosts[score.value])
  score.value--
}

function updateAncestryBonus(event) {
  const newValue = event.target.value
  if (isNaN(Number(newValue))) {
    ancestryBonus.value = 0
    return
  }
  if (newValue.length > 1) {
    ancestryBonus.value = newValue.slice(0, 1)
    return
  }
  ancestryBonus.value = newValue
}

function ancestryBonusFocusOut(event) {
  if (event.target.value === '') ancestryBonus.value = 0
}
</script>

<template>
  <tr class="border-b border-emerald-700">
    <td class="p-2 md:p-3">{{ name }}</td>

    <StatControls :score="score" @increaseScore="increaseScore" @decreaseScore="decreaseScore" />

    <td class="p-3 text-center">
      +&nbsp;
      <input
        class="bg-emerald-950 p-2 rounded w-10 text-center"
        type="text"
        :value="ancestryBonus"
        @input="updateAncestryBonus"
        @focusout="ancestryBonusFocusOut"
      />
    </td>

    <td class="p-3 text-center">
      {{ finalScore }} ({{ modifier > 0 ? `+${modifier}` : modifier }})
    </td>
  </tr>
</template>
