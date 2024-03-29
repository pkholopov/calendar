<template>
  <div class="calendar__header">
    <div class="calendar__header-month">
      <button class="calendar__header-button" @click="$emit('prevMonth')">&#8592;</button>
      <span>{{ months[month] }} {{ year }}</span>
      <button class="calendar__header-button" @click="$emit('nextMonth')">&#8594;</button>
    </div>
    <div class="calendar__header-days">
      <span v-for="day in daysOfWeek">{{ day }}</span>
    </div>
  </div>
</template>

<script setup>
import { localization } from '@/utils/localization'
import { useLocaleStore } from '@/stores/locale.js'
import { storeToRefs } from 'pinia';
import { computed } from 'vue';

const { locale } = storeToRefs(useLocaleStore())

const props = defineProps({
  month: {
    type: Number,
  },
  year: {
    type: Number,
  }
})

const months = computed(() => localization[locale.value].months)

const daysOfWeek  = computed(() => localization[locale.value].daysOfWeek)

</script>

<style scoped>
.calendar__header {
  display: flex;
  flex-direction: column;
}
.calendar__header-month{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  font-size: 1.2rem;
}

.calendar__header-button{
  border: none;
  background-color: transparent;
  cursor: pointer;
}

.calendar__header-days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  justify-items: center;
  align-items: center;
  padding: 10px;
  font-size: 1.2rem;
}
</style>
