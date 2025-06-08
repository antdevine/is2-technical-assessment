<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
const emit = defineEmits(['radioUpdated']);
const props = withDefaults(defineProps<{
    radioOptions?: { value: string, name?: string }[],
    legendText?: string,
    checked: string
}>(), {
    radioOptions: () => [
    { value: 'Yes', name: 'option' },
    { value: 'No' },
    { value: 'option' }
  ],
    legendText: 'Radio Question',
});

const radioSelected = (event: Event) => {
    const target = event.target as HTMLInputElement;
    emit('radioUpdated', target.value);
};
</script>

<template>
    <fieldset>
        <legend>{{ legendText }}</legend>
        <label v-for="(option, index) in radioOptions" :key="index">
          <input type="radio" @change="radioSelected" :name="option.name || 'option'" :value="option.value" required :checked="checked === option.value" />
          {{ option.value }}
        </label>
      </fieldset>
</template>