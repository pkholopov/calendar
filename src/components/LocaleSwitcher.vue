<template>
  <select v-model="locale" @change="changeLocale(locale)">
    <option value="ru">Русский</option>
    <option value="en">English</option>
  </select>
</template>

<script setup>
import { useLocaleStore } from '@/stores/locale'
import { storeToRefs } from 'pinia';

const { locale } = storeToRefs(useLocaleStore())
const { changeLocale } = useLocaleStore()

</script>

<style scoped>

</style>
