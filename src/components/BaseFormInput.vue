<script setup>
import { useId, useTemplateRef } from 'vue'
import ErrorComponent from './ErrorComponent.vue'

defineEmits(['blur-event'])
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

const model = defineModel()
const id = useId()
const errorId = useId()
const input = useTemplateRef('input')

// Focus on the ref
function focusInput() {
  input.value?.focus()
}

//Exposes the focus to the parent component
defineExpose({
  focusInput,
})
</script>

<template>
  <div>
    <label :for="id" class="text-body-md-regular"
      >{{ label }}<span class="star" aria-hidden="true">*</span></label
    >
    <input
      class="text-body-md-regular"
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
input {
  padding: 0.5rem;
}

div {
  display: flex;
  flex-direction: column;
  flex: 1;
}
</style>
