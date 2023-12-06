<script setup>
import { inject } from 'vue'
import defaults from '../defaults'

const { points } = inject('points')
</script>

<template>
  <h1 class="text-3xl">💰 D&D Point Shop (Vue)</h1>
  <p class="p-2">🪙 Current points: {{ points }}/{{ defaults.maxPoints }}</p>
</template>
