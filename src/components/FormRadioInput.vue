<script setup>
const emit = defineEmits(['blur-event'])
import { useId } from 'vue'
import SharedContainerSlot from './SharedContainerSlot.vue'
import ErrorComponent from './ErrorComponent.vue'

const model = defineModel()
const errorId = useId()
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

function onFocusOut(event) {
  const next = event.relatedTarget

  if (!next || !event.currentTarget.contains(next)) {
    emit('blur-event')
  }
}
</script>

<template>
  <fieldset @focusout="onFocusOut" :aria-invalid="!!error">
    <legend class="text-body-sm">{{ legend }}<span class="star" aria-hidden="true">*</span></legend>
    <SharedContainerSlot>
      <label v-for="(option, index) in options" :key="option.value" class="text-body-sm">
        <input
          type="radio"
          :value="option.value"
          :name="name"
          v-model="model"
          :aria-describedby="index === 0 && error ? errorId : undefined"
          required
        />
        {{ option.label }}
      </label>
    </SharedContainerSlot>
    <ErrorComponent :label="legend" :error="error" :error-id="errorId" />
  </fieldset>
</template>

<style scoped>
label {
  border: 1px solid var(--color-grey-500);
  display: flex;
  align-items: center;
  gap: 1rem;
  flex: 1;
  padding-left: 1.5rem;
  border-radius: 0.5rem;
}
</style>
