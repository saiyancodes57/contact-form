<script setup>
const model = defineModel()
defineEmits(['blur-event'])
defineProps({
  labelText: {
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
      <input type="checkbox" :name="name" v-model="model" @blur="$emit('blur-event')" />
      {{ labelText }}<span>*</span>
    </label>
    <p class="error-text">{{ error }}</p>
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
