<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
const emit = defineEmits(["radioUpdated"]);
const props = withDefaults(
  defineProps<{
    radioOptions?: { value: string; name?: string }[];
    legendText?: string;
    checked: string;
  }>(),
  {
    radioOptions: () => [
      { value: "Yes", name: "option" },
      { value: "No" },
      { value: "option" },
    ],
    legendText: "Radio Question",
  }
);

const radioSelected = (event: Event) => {
  const target = event.target as HTMLInputElement;
  emit("radioUpdated", target.value);
};
</script>

<template>
  <fieldset class="flex gap-4 flex-wrap">
    <legend class="block text-md font-semibold mb-2">{{ legendText }} <span class="text-red-500">*</span></legend>
    <label
      v-for="(option, index) in radioOptions"
      :key="index"
      class="flex-1 cursor-pointer"
    >
      <input
        type="radio"
        @change="radioSelected"
        :name="option.name || 'option'"
        :value="option.value"
        required
        :checked="checked === option.value"
        class="sr-only peer"
      />
      <span
        class="block w-full text-center px-4 py-2 border border-gray-300 rounded-lg transition peer-checked:bg-purple-100 peer-checked:border-purple-500 peer-checked:text-purple-700"
      >
        {{ option.value }}
      </span>
    </label>
  </fieldset>
</template>
