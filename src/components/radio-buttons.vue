<script setup>
const emit = defineEmits(['radioUpdated']);
const props = defineProps({
    radioOptions: {
        type: Array,
        default: () => [{value: 'Yes', name: 'option'}, 'No', 'option']
    },
    legendText: {
        type: String,
        default: 'Radio Question'
    },
    checked: {
        type: String,
        default: ''
    }
});

const radioSelected = (event) => {
    emit('radioUpdated', event.target.value);
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