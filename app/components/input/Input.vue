<template>
  <div class="input-wrapper">
    <label
      v-if="label"
      :for="id"
      class="input-wrapper__label"
    >
      {{ label }}
    </label>

    <div class="relative flex">
      <input
        v-model="modelValue"
        :id="id"
        :type="type"
        :placeholder="placeholder"
        :disabled="disabled"
        :readonly="readonly"
        class="input-wrapper__input"
        :class="{
          'input-wrapper__input--clearable': showClearable,
          'input-wrapper__input--error': error,
        }"
      />

      <font-awesome-icon
        v-if="showClearable"
        icon="fa-xmark"
        class="input-wrapper__clear"
        @click="clearInput"
      />
    </div>

    <span
      v-if="errorMessage"
      class="input-wrapper__error-message"
    >
      {{ errorMessage }}
    </span>
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";
import type { InputHTMLAttributes } from "vue";

type InputTypes = Extract<
  InputHTMLAttributes["type"],
  "text" | "number" | "email" | "password" | "tel" | "url"
>;

interface InputProps {
  id?: string;
  label?: string;
  type?: InputTypes;
  placeholder?: string;
  disabled?: boolean;
  readonly?: boolean;
  clearable?: boolean;
  errorMessage?: string;
  error?: boolean;
}

const props = withDefaults(defineProps<InputProps>(), {
  label: "",
  type: "text",
  placeholder: "",
  errorMessage: "",
});

const modelValue = defineModel<InputHTMLAttributes["value"]>();

const showClearable = computed(() => {
  return props.clearable && modelValue.value && !props.disabled;
});

function clearInput() {
  if (!props.clearable) return;
  modelValue.value = undefined;
}
</script>

<style scoped>
@import "@/components/input/input.css";
</style>


