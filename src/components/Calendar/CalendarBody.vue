<template>
  <div class="calendar__body">
    <span v-for="day in days" class="calendar__body-day" :class="{'calendar__body-day-current': (currentDay && day === currentDay)}" @click="$emit('selectDay', day)">{{ day }}</span>
  </div>
</template>

<script setup>
defineProps({
  days: {
    type: Array,
    requared: true,
  },
  currentDay: {
    type: Number,
    requared: false,
  }
})
</script>

<style scoped>
.calendar__body{
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  justify-items: center;
  align-items: center;
  padding: 10px;
  font-size: 1.2rem;
}

.calendar__body-day{
  width: 100%;
  border: 1px solid transparent;
  text-align: center;
  cursor: pointer;
}

.calendar__body-day:hover {
  border: 1px solid gray;
}

.calendar__body-day-current {
  background: #c0c0c0;
}
</style>
