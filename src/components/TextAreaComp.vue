<script setup>
import { useId } from 'vue'

const model = defineModel()
defineEmits(['blur-event'])
const id = useId()
const errorId = useId()
defineProps({
  label: {
    type: String,
    required: true,
  },
  error: {
    type: String,
  },
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
    ></textarea>
    <p class="error-text" :id="errorId">{{ error }}</p>
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-direction: column;
}

textarea {
  border-radius: 0.5rem;
  resize: vertical;
  border: 1px solid var(--color-grey-500);
}
</style>
