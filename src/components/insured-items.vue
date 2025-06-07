<script setup>
const props = defineProps({
  items: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['update:items']);

const updateItem = (index, value) => {
  const updated = [...props.items];
  updated[index] = value;
  emit('update:items', updated);
};

const removeItem = (index) => {
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
        @input="updateItem(index, $event.target.value)"
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
    <button type="button" @click.prevent="addItem">Add another</button>
  </fieldset>
</template>
