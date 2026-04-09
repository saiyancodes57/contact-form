<script setup>
const model = defineModel()
defineEmits(['blur-event'])
defineProps({
  id: {
    type: String,
    required: true,
  },
  labelText: {
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
    <label :for="id" class="text-body-sm">{{ labelText }}<span class="star">*</span></label>
    <textarea :id="id" rows="7" v-model="model" @blur="$emit('blur-event')" required></textarea>
    <p class="error-text">{{ error }}</p>
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
