<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
const props = defineProps<{
    selected: string,
  options: { value: string, label: string }[];
}>();

const emit = defineEmits(['limitUpdated']);
const limitSelected = (event: Event) => {
  const target = event.target as HTMLSelectElement;
  emit('limitUpdated', target.value);
};
</script>

<template>
  <div>
    <label for="limitSelect">Limit of Indemnity</label>
    <select
      id="limitSelect"
      :value="selected"
      @change="limitSelected"
      required
    >
      <option disabled value="">Please select</option>
      <option v-for="opt in options" :key="opt.value" :value="opt.value">
        {{ opt.label }}
      </option>
    </select>
  </div>
</template>
