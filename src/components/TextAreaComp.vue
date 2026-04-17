<script setup>
import { useId, useTemplateRef } from 'vue'
import ErrorComponent from './ErrorComponent.vue'

defineEmits(['blur-event'])
defineProps({
  label: {
    type: String,
    required: true,
  },
  error: {
    type: String,
  },
})

const model = defineModel()
const id = useId()
const errorId = useId()
const textarea = useTemplateRef('message')

function focusInput() {
  textarea.value?.focus()
}

defineExpose({
  focusInput,
})
</script>

<template>
  <div class="textarea">
    <label :for="id" class="text-body-sm"
      >{{ label }}<span class="star" aria-hidden="true">*</span></label
    >
    <textarea
      :id="id"
      rows="7"
      v-model="model"
      @blur="$emit('blur-event')"
      :aria-describedby="error ? errorId : undefined"
      :aria-invalid="!!error"
      required
      ref="message"
    ></textarea>
    <ErrorComponent :label="label" :error="error" :error-id="errorId" />
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-direction: column;
}

textarea {
  border-radius: 0.5rem;
  padding: 0.5rem;
  resize: vertical;
  border: 1px solid var(--color-grey-500);
}
</style>
