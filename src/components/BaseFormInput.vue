<script setup>
import { useId, useTemplateRef } from 'vue'
import ErrorComponent from './ErrorComponent.vue'

defineEmits(['blur-event'])
const model = defineModel()
const id = useId()
const errorId = useId()
const input = useTemplateRef('input')

defineProps({
  label: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    default: 'text',
  },
  autocomplete: {
    type: String,
  },
  error: {
    type: String,
  },
})

function focusInput() {
  input.value?.focus()
}

defineExpose({
  focusInput,
})
</script>

<template>
  <div>
    <label :for="id" class="text-body-sm"
      >{{ label }}<span class="star" aria-hidden="true">*</span></label
    >
    <input
      :type="type"
      :id="id"
      v-model="model"
      :autocomplete="autocomplete"
      @blur="$emit('blur-event')"
      :aria-describedby="error ? errorId : undefined"
      :aria-invalid="!!error"
      ref="input"
      required
    />
    <ErrorComponent :label="label" :error="error" :error-id="errorId" />
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  flex: 1;
}
</style>
