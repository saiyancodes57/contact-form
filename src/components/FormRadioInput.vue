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
  <fieldset @focusout="onFocusOut" :aria-invalid="!!error" ref="radio-fieldset">
    <legend class="text-body-sm">{{ legend }}<span class="star" aria-hidden="true">*</span></legend>
    <SharedContainerSlot>
      <label v-for="(option, index) in options" :key="option.value" class="text-body-sm">
        <input
          type="radio"
          :value="option.value"
          :name="name"
          v-model="model"
          :aria-describedby="index === 0 && error ? errorId : undefined"
          :ref="index === 0 ? 'first-option' : undefined"
          required
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
}

fieldset[aria-invalid='true'] input[type='radio']:focus {
  outline: 2px solid;
  outline-offset: 2px;
}
</style>
