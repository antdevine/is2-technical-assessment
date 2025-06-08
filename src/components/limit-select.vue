<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
const props = defineProps<{
  selected: string;
  options: { value: string; label: string }[];
}>();

const emit = defineEmits(["limitUpdated"]);
const limitSelected = (event: Event) => {
  const target = event.target as HTMLSelectElement;
  emit("limitUpdated", target.value);
};
</script>

<template>
  <div>
    <label for="limitSelect" class="block text-md font-semibold mb-1"
      >Limit of Indemnity <span class="text-red-500">*</span></label
    >
    <select
      id="limitSelect"
      :value="selected"
      @change="limitSelected"
      required
      class="w-full rounded-lg border border-gray-300 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-purple-500"
    >
      <option disabled value="">Please select</option>
      <option v-for="opt in options" :key="opt.value" :value="opt.value">
        {{ opt.label }}
      </option>
    </select>
  </div>
</template>
