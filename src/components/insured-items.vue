<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
import { Trash2 } from "lucide-vue-next";
import BaseButton from "./base-button.vue";

const props = defineProps<{
  items: string[];
}>();

const emit = defineEmits<{
  (event: "update:items", value: string[]): void;
}>();

const updateItem = (index: number, value: string) => {
  const updated = [...props.items];
  updated[index] = value;
  emit("update:items", updated);
};

const removeItem = (index: number) => {
  const updated = [...props.items];
  updated.splice(index, 1);
  emit("update:items", updated);
};

const addItem = () => {
  emit("update:items", [...props.items, ""]);
};
</script>

<template>
  <fieldset>
    <div class="mt-4" v-for="(item, index) in items" :key="index">
      <label :for="`item-${index}`" class="block text-md font-semibold mb-2"
        >Item {{ index + 1 }} <span class="text-red-500">*</span></label
      >
      <div class="flex items-center gap-2">
        <input
          :id="`item-${index}`"
          :placeholder="`Item ${index + 1}`"
          :value="item"
          @input="updateItem(index, ($event.target as HTMLInputElement).value)"
          required
          type="text"
          aria-label="Item description"
          class="w-full rounded-lg border border-gray-300 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-purple-500"
        />
        <BaseButton
          @click.prevent="removeItem(index)"
          v-if="items.length > 1"
          type="button"
          aria-label="Remove item"
          classes=""
        >
          <Trash2 class="w-5 h-5 text-red-500 cursor-pointer" />
        </BaseButton>
      </div>
    </div>

    <BaseButton
      @click.prevent="addItem"
      v-if="items[items.length - 1].length > 0"
      type="button"
      aria-label="Add item"
    >
      Add another
    </BaseButton>
  </fieldset>
</template>
