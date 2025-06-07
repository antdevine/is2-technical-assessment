<script setup>
const props = defineProps({
    selected: String,
  options: {
    type: Array,
    default: () => []
  }
});
const emit = defineEmits(['limitUpdated']);
const limitSelected = (event) => {
  emit('limitUpdated', event.target.value);
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
