<script setup>
import { useId } from 'vue'
defineEmits(['blur-event'])
const model = defineModel()
const id = useId()
const errorId = useId()

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
    />
    <p class="error-text" :id="errorId" aria-live="assertive">{{ error }}</p>
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  flex: 1;
}
</style>
