<script setup>
const emit = defineEmits(['dateUpdated']);

const today = new Date();
const minDate = today.toISOString().split('T')[0];

const futureDate = new Date();
futureDate.setDate(today.getDate() + 15);
const maxDate = futureDate.toISOString().split('T')[0];

const dateSelected = (event) => {
    emit('dateUpdated', event.target.value);
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