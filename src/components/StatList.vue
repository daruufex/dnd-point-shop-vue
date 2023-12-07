<script setup>
import StatItem from './StatItem.vue'

const statNames = ['Strength', 'Dexterity', 'Constitution', 'Intelligence', 'Wisdom', 'Charisma']
</script>

<template>
  <table classe="w-full text-md md:text-xl">
    <thead>
      <tr class="border-b-2 border-b-emerald-700">
        <th class="p-2 md:p-3 text-left">Attribute</th>
        <th class="p-2 md:p-3 text-center">Ability score</th>
        <th class="p-2 md:p-3 text-center">Ancestry bonus</th>
        <th class="p-2 md:p-3 text-center">Final score</th>
      </tr>
    </thead>

    <tbody>
      <StatItem v-for="stat in statNames" :key="stat" :name="stat" />
    </tbody>
  </table>
</template>
