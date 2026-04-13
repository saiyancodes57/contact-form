<script setup>
import { useId } from 'vue'
import ErrorComponent from './ErrorComponent.vue'

const model = defineModel()
defineEmits(['blur-event'])
const errorId = useId()
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
      />
      {{ label }}<span aria-hidden="true">*</span>
    </label>
    <!-- <p class="error-text" :id="errorId">{{ error }}</p>-->
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
</style>
