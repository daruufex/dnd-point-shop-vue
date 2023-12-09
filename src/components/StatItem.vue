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
</script>

<template>
  <tr class="border-b border-emerald-700">
    <td class="p-2 md:p-3">{{ name }}</td>

    <StatControls :score="score" @increaseScore="increaseScore" @decreaseScore="decreaseScore" />
    <AncestryBonus v-model="ancestryBonus" />

    <td class="p-3 text-center">
      {{ finalScore }} ({{ modifier > 0 ? `+${modifier}` : modifier }})
    </td>
  </tr>
</template>
