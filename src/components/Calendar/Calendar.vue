<template>
  <div class="calendar">
    <CalendarHeader :month :year @prevMonth="prevMonth" @nextMonth="nextMonth"/>
    <CalendarBody :days :currentDay @selectDay="selectDay"/>
  </div>
</template>

<script setup>
import CalendarHeader from './CalendarHeader.vue';
import CalendarBody from './CalendarBody.vue';
import { computed, ref, watch } from 'vue'

const prop = defineProps({
  setDate: {
    type: String
  }
})

const emit = defineEmits(['selectDate'])

const date = ref(prop.setDate ? new Date(prop.setDate) : new Date())
const month = ref(date.value.getMonth())
const year = ref(date.value.getFullYear())

const currentDay = computed(() => {
  if(date.value.getMonth() !== month.value || date.value.getFullYear() !== year.value) return 0
  return date.value.getDate()
})

const days = computed(() => {
  const daysInMonth = new Date(year.value, month.value + 1, 0).getDate()
  const firstDay = new Date(year.value, month.value, 0).getDay()
  const daysArray = []
  for(let i = 0; i < firstDay; i++) {
    daysArray.push('')
  }
  for(let i = 1; i <= daysInMonth; i ++){
    daysArray.push(i)
  }
  return daysArray
})

watch(() => prop.setDate, (newValue) => {
  newValue ? date.value = new Date(newValue) : date.value = new Date()
  month.value = date.value.getMonth()
  year.value = date.value.getFullYear()
})

const prevMonth = () => {
  if(month.value === 0) {
    month.value = 11
    year.value--
  } else {
    month.value--
  }
}

const nextMonth = () => {
  if(month.value === 11){
    month.value = 0
    year.value++
  } else {
    month.value++
  }
}

const selectDay = (day) => {
  const date = `${year.value}-${month.value+1}-${day}`
  emit('selectDate', date)
}
</script>

<style scoped>
.calendar{
  width: 400px;
}
</style>
