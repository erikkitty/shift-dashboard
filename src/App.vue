<template>
  <div id="app">
    <h1>Shift Dashboard</h1>
    <button @click="isListVisible = !isListVisible">
      {{ isListVisible ? "Скрыть список" : "Показать список" }}
    </button>
    <button @click="clearShifts">Очистить</button>
    <p v-if="shifts.lenght === 0">Смен пока нет</p>
    <ul v-show="isListVisible">
      <li v-for="shift in shifts" :key="shift.id">
        <strong>{{ shift.title }}</strong>
        <span>{{ shift.date }} {{ shift.start }}-{{ shift.end }}</span>
        <span
          :class="{
            'status-approved': shift.status === 'approved',
            'status-declined': shift.status === 'declined',
            'status-pending': shift.status === 'pending',
          }"
          >{{ shift.status }}</span
        >
        <span>{{ shift.hours * shift.hourlyRate }}$</span>
      </li>
    </ul>
  </div>
</template>

<script>
import shifts from "@/data/mockShifts.js";
export default {
  name: "App",
  data() {
    return {
      shifts: shifts,
      isListVisible: true,
    };
  },
  methods: {
    clearShifts() {
      this.shifts = [];
    },
  },
};
</script>

<style>
.status-approved {
  color: green;
  font-weight: bold;
}

.status-declined {
  color: red;
  text-decoration: line-through;
}

.status-pending {
  color: orange;
}
</style>
