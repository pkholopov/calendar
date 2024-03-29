<template>
  <div class="app">
    <Calendar :set-date="date" @select-date="selectDate"/>
    <LocaleSwitcher />
    <input type="text" v-model.lazy.trim="date" />
  </div>
</template>

<script setup>
import Calendar from './components/Calendar/Calendar.vue'
import LocaleSwitcher from '@/components/LocaleSwitcher.vue'
import { ref } from 'vue'

const date = ref('')

const selectDate = (value) => {
  date.value = value
}
</script>

<style scoped>
.app{
  display: flex;
  align-items: baseline;
}
</style>
