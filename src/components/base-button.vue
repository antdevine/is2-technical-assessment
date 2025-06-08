<script setup lang="ts">
import {
  computed,
  defineEmits,
  defineOptions,
  defineProps,
  withDefaults,
} from "vue";
const emit = defineEmits<{
  (e: "click", event: MouseEvent): void;
}>();

const props = withDefaults(
  defineProps<{
    type?: "button" | "submit";
    disabled?: boolean;
    ariaLabel?: string;
    classes?: string;
  }>(),
  {
    classes:
      "w-full py-3 mt-4 bg-gradient-to-r from-purple-600 to-orange-500 text-white rounded-xl text-lg font-semibold hover:brightness-110 transition disabled:opacity-50",
  }
);

defineOptions({ inheritAttrs: false });

const buttonClasses = computed(() => {
  const buttonDissabled = props.disabled
    ? "cursor-not-allowed"
    : "cursor-pointer";
  return `${props.classes} ${buttonDissabled}`;
});
</script>

<template>
  <button
    :type="type"
    :disabled="disabled"
    :class="buttonClasses"
    :aria-disabled="disabled"
    :aria-label="ariaLabel"
    @click="(e) => emit('click', e)"
  >
    <slot />
  </button>
</template>
