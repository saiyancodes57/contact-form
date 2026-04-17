<script setup>
import { useId, useTemplateRef } from 'vue'
import ErrorComponent from './ErrorComponent.vue'

defineEmits(['blur-event'])
defineProps({
  label: {
    type: String,
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
const checkbox = useTemplateRef('checkbox')

function focusInput() {
  checkbox.value?.focus()
}

defineExpose({
  focusInput,
})
</script>

<template>
  <div class="consent-checkbox">
    <label class="text-body-sm">
      <input
        type="checkbox"
        :name="name"
        v-model="model"
        @blur="$emit('blur-event')"
        :aria-describedby="error ? errorId : undefined"
        :aria-invalid="!!error"
        required
        ref="checkbox"
      />
      {{ label }}<span aria-hidden="true">*</span>
    </label>
    <ErrorComponent :label="label" :error="error" :error-id="errorId" />
  </div>
</template>

<style scoped>
label {
  display: flex;
  align-items: center;
  gap: 1rem;
}

span {
  color: var(--color-green-600);
}

input[type='checkbox']:focus {
  outline: 2px solid;
  outline-offset: 2px;
}
</style>
