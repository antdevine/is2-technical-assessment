<script setup lang="ts">
import { defineEmits } from 'vue';
const emit = defineEmits(['dateUpdated']);

const today = new Date();
const minDate = today.toISOString().split('T')[0];

const futureDate = new Date();
futureDate.setDate(today.getDate() + 15);
const maxDate = futureDate.toISOString().split('T')[0];

const dateSelected = (event: Event) => {
  const target = event.target as HTMLInputElement;
    emit('dateUpdated', target.value);
};
</script>

<template>
    <label for="startDate">Start Date</label>
        <input
          type="date"
          id="startDate"
          @change="dateSelected"
          :min="minDate"
          :max="maxDate"
          required
        />
</template>