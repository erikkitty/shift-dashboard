<template>
  <div class="shift-card">
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
    <div v-if="showActions" class="shift-card__actions">
      <button @click="approve">Одобрить</button>
      <button @click="decline">Отклонить</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "ShiftCard",
  props: {
    shift: {
      type: Object,
      required: true,
    },
    showActions: {
      type: Boolean,
      default: true,
    },
  },
  methods: {
    approve() {
      this.$emit("approve", this.shift.id);
    },
    decline() {
      this.$emit("decline", this.shift.id);
    },
  },
};
</script>
<style scoped>
.shift-card {
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 12px;
  margin-bottom: 8px;
  display: flex;
  gap: 12px;
  align-items: center;
}

.shift-card__actions {
  margin-left: auto;
  display: flex;
  gap: 8px;
}

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
