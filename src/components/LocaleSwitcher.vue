<template>
  <select v-model="locale" @change="changeLocale(locale)">
    <option value="ru">Русский</option>
    <option value="en">English</option>
  </select>
</template>

<script setup>
import { useLocaleStore } from '@/stores/locale'

const { locale, changeLocale } = useLocaleStore()

</script>

<style scoped>

</style>
