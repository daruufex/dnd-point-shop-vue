<script setup>
import { inject, computed } from 'vue'

import defaults from '../defaults'
import StatButton from './StatButton.vue'

const props = defineProps(['score'])

const { points } = inject('points')

const scoreClasses = computed(() => {
  if (props.score === defaults.maxScore) return 'font-bold text-green-100'
  if (props.score === defaults.minScore) return 'italic text-red-200'
  else return ''
})
</script>

<template>
  <td class="p-2 md:p-3 flex justify-center items-center gap-4">
    <span :class="scoreClasses">{{ score }}</span>
    <div class="inline-flex flex-col items-start gap-2">
      <div class="whitespace-nowrap">
        <StatButton
          @increaseScore="$emit('increaseScore')"
          :disabled="score === defaults.maxScore || defaults.scoreCosts[score + 1] > points"
        >
          +
        </StatButton>
        <span :class="`text-xs ${defaults.scoreCosts[score + 1] > points ? 'text-red-400' : ''}`">
          {{ score < defaults.maxScore ? `-${defaults.scoreCosts[score]}🪙` : '' }}
        </span>
      </div>
      <div class="whitespace-nowrap">
        <StatButton @increaseScore="$emit('decreaseScore')" :disabled="score === defaults.minScore">
          -
        </StatButton>
        <span class="text-xs">
          {{ score > defaults.minScore ? `+${defaults.scoreCosts[score]}🪙` : '' }}
        </span>
      </div>
    </div>
  </td>
</template>
