<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
import { Trash2 } from "lucide-vue-next";
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
        <button
          v-if="items.length > 1"
          type="button"
          @click.prevent="removeItem(index)"
          aria-label="Remove item"
        >
          <Trash2 class="w-5 h-5 text-red-500 cursor-pointer" />
        </button>
      </div>
    </div>
    <button
      type="button"
      v-if="items[items.length - 1].length > 0"
      @click.prevent="addItem"
      class="w-full py-3 mt-4 bg-gradient-to-r from-purple-600 to-orange-500 text-white rounded-xl text-lg font-semibold hover:brightness-110 transition disabled:opacity-50 cursor-pointer"
    >
      Add another
    </button>
  </fieldset>
</template>
