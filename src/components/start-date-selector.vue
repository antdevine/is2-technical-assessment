<script setup lang="ts">
import { defineEmits } from "vue";
const emit = defineEmits(["dateUpdated"]);

const today = new Date();
const minDate = today.toISOString().split("T")[0];

const futureDate = new Date();
futureDate.setDate(today.getDate() + 15);
const maxDate = futureDate.toISOString().split("T")[0];

const dateSelected = (event: Event) => {
  const target = event.target as HTMLInputElement;
  emit("dateUpdated", target.value);
};
</script>

<template>
  <label for="startDate" class="block text-md font-semibold mb-1"
    >Start Date <span class="text-red-500">*</span></label
  >
  <input
    type="date"
    id="startDate"
    @change="dateSelected"
    :min="minDate"
    :max="maxDate"
    required
    class="w-full rounded-lg border border-gray-300 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-purple-500"
  />
</template>
