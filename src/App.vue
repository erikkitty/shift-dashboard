<template>
  <div id="app">
    <h1>Shift Dashboard</h1>

    <button @click="isListVisible = !isListVisible">
      {{ isListVisible ? "Скрыть список" : "Показать список" }}
    </button>

    <button @click="clearShifts">Очистить</button>

    <p v-if="shifts.length === 0">Смен пока нет</p>
    <div v-show="isListVisible">
      <ShiftCard
        v-for="shift in shifts"
        :key="shift.id"
        :shift="shift"
        :show-actions="shift.status === 'pending'"
        @approve="approveShift"
        @decline="declineShift"
      ></ShiftCard>
    </div>
  </div>
</template>

<script>
import shifts from "@/data/mockShifts.js";
import ShiftCard from "./components/ShiftCard.vue";
export default {
  name: "App",
  components: { ShiftCard },
  data() {
    return {
      shifts,
      isListVisible: true,
    };
  },
  methods: {
    clearShifts() {
      this.shifts = [];
    },
    approveShift(id) {
      this.setStatus(id, "approved");
    },
    declineShift(id) {
      this.setStatus(id, "declined");
    },
    setStatus(id, status) {
      const shift = this.shifts.find((s) => s.id === id);
      if (shift) {
        shift.status = status;
      }
    },
  },
};
</script>
