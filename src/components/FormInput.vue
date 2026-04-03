<script setup>
defineProps({
  label: String,
  id: String,
  inputType: {
    type: String,
    default: 'text',
  },
  name: {
    type: String,
    required: false,
  },
})
</script>

<template>
  <div v-if="inputType !== 'radio'" class="input-group">
    <label :for="id" class="text-body-sm">{{ label }}<span class="star">*</span></label>
    <input :type="inputType" :id="id" :name="name" />
  </div>

  <div v-else class="input-group">
    <label :for="id" class="text-body-sm radio-container">
      <input :type="inputType" :id="id" :name="name" />
      <span :id="id" class="text-body-sm">{{ label }}</span>
    </label>
  </div>
</template>

<style scoped>
/* For any input not a radio or checkbox */
input:not([type='radio'], [type='checkbox']) {
  height: 3rem;
  border-radius: 0.5rem;
  border: 1px solid var(--color-grey-500);
}

.input-group:has(input[type='checkbox']) {
  display: flex;
  justify-content: flex-end;
  flex-direction: row-reverse;
  gap: 1rem;
}

.input-group:has(input[type='checkbox']) {
  display: flex;
  justify-content: flex-end;
  flex-direction: row-reverse;
  gap: 1rem;
}

.radio-container {
  border: 1px solid var(--color-grey-500);
  height: 3rem;
  border-radius: 0.5rem;
  display: flex;
  align-items: center;
  padding: 1rem;
  gap: 1rem;
}
</style>
