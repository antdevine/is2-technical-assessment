<script setup lang="ts">
import { ref, defineEmits } from "vue";
import Flatpickr from "vue-flatpickr-component";
import "flatpickr/dist/themes/airbnb.css";

const emit = defineEmits(["dateUpdated"]);

const selectedDate = ref(null);
const today = new Date();
const futureDate = new Date();
futureDate.setDate(today.getDate() + 15);

const config = {
  dateFormat: "d/m/Y",
  minDate: today,
  maxDate: futureDate,
};
</script>

<template>
  <label for="startDate" class="block text-md font-semibold mb-1">
    Start Date <span class="text-red-500">*</span>
  </label>

  <Flatpickr
    v-model="selectedDate"
    :config="config"
    class="w-full border px-4 py-2 rounded-lg focus:ring-purple-500 focus:outline-none"
    @on-change="emit('dateUpdated', selectedDate)"
    id="startDate"
    placeholder="Select start date"
    :aria-label="'Start Date'"
    :aria-required="true"
  />
</template>
