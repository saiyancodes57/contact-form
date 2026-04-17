<script setup>
const emit = defineEmits(['blur-event'])
import { useId, useTemplateRef } from 'vue'
import SharedContainerSlot from './SharedContainerSlot.vue'
import ErrorComponent from './ErrorComponent.vue'

defineProps({
  legend: {
    type: String,
    required: true,
  },
  options: {
    type: Array,
    required: true,
  },
  name: {
    type: String,
    required: true,
  },
  error: {
    type: String,
  },
})

const model = defineModel()
const errorId = useId()
const fieldsetRef = useTemplateRef('radio-fieldset')

function focusInput() {
  const input = fieldsetRef.value?.querySelector('input')
  input?.focus()
}

defineExpose({
  focusInput,
})

function onFocusOut() {
  emit('blur-event')
}
</script>

<template>
  <fieldset
    @focusout="onFocusOut"
    ref="radio-fieldset"
    :aria-describedby="index === 0 && error ? errorId : undefined"
    required
  >
    <legend class="text-body-md-regular">
      {{ legend }}<span class="star" aria-hidden="true">*</span>
    </legend>
    <SharedContainerSlot>
      <label v-for="(option, index) in options" :key="option.value" class="text-body-md-regular">
        <input
          type="radio"
          :value="option.value"
          :name="name"
          v-model="model"
          :ref="index === 0 ? 'first-option' : undefined"
        />
        {{ option.label }}
      </label>
    </SharedContainerSlot>
    <ErrorComponent :label="legend" :error="error" :error-id="errorId" />
  </fieldset>
</template>

<style scoped>
legend {
  color: var(--color-grey-900);
  margin-bottom: 1rem;
}

label {
  border: 1px solid var(--color-grey-500);
  display: flex;
  align-items: center;
  gap: 1rem;
  flex: 1;
  padding-left: 1.5rem;
  border-radius: 0.5rem;

  &:has(input:checked) {
    border: 1px solid var(--color-green-600);
    background-color: var(--color-green-200);
  }
}
input {
  accent-color: var(--color-green-600);
  width: 1.25rem;
}

fieldset[aria-invalid='true'] input[type='radio']:focus-visible {
  outline: 2px solid;
  outline-offset: 2px;
}
</style>
