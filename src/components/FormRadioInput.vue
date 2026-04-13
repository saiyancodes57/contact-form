<script setup>
defineEmits(['blur-event'])
import { useId } from 'vue'
import SharedContainerSlot from './SharedContainerSlot.vue'
const model = defineModel()
const errorId = useId()
defineProps({
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
</script>

<template>
  <fieldset
    @focusout="$emit('blur-event')"
    :aria-describedby="error ? errorId : undefined"
    :aria-invalid="!!error"
  >
    <legend class="text-body-sm">Query Type<span class="star" aria-hidden="true">*</span></legend>
    <SharedContainerSlot>
      <label v-for="option in options" :key="option.value" class="text-body-sm">
        <input type="radio" :value="option.value" :name="name" v-model="model" />
        {{ option.label }}
      </label>
    </SharedContainerSlot>
    <p class="error-text" :id="errorId">{{ error }}</p>
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
