<script setup>
import { ref, provide } from 'vue'

import defaults from './defaults'
import AppHeader from './components/AppHeader.vue'
import StatList from './components/StatList.vue'

const points = ref(defaults.startingPoints)

function setPoints(newPoints) {
  points.value = newPoints
}

provide('points', { points, setPoints })
</script>

<template>
  <div class="container max-w-3xl mx-auto p-2 pt-6 md:p-4">
    <AppHeader />
    <StatList />
  </div>
</template>
