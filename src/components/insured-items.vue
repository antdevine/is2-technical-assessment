<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
const props = defineProps<{
  items: string[];
}>();

const emit = defineEmits<{
  (event: 'update:items', value: string[]): void;
}>();

const updateItem = (index: number, value: string) => {
  const updated = [...props.items];
  updated[index] = value;
  emit('update:items', updated);
};

const removeItem = (index: number) => {
  const updated = [...props.items];
  updated.splice(index, 1);
  emit('update:items', updated);
};

const addItem = () => {
  emit('update:items', [...props.items, '']);
};
</script>

<template>
  <fieldset>
    <legend>Items to Insure</legend>
    <div
      v-for="(item, index) in items"
      :key="index"
    >
      <label :for="`item-${index}`">Item {{ index + 1 }}</label>
      <input
        :id="`item-${index}`"
        :placeholder="`Item ${index + 1}`"
        :value="item"
        @input="updateItem(index, ($event.target as HTMLInputElement).value)"
      />
      <button
        v-if="items.length > 1"
        type="button"
        @click.prevent="removeItem(index)"
        aria-label="Remove item"
      >
        Remove
      </button>
    </div>
    <button type="button" v-if="items[items.length - 1].length > 0" @click.prevent="addItem">Add another</button>
  </fieldset>
</template>
