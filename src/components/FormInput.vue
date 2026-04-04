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
  value: {
    type: String,
    required: false,
  },
})

const model = defineModel()
</script>

<template>
  <div v-if="inputType !== 'radio'" class="input-group">
    <label :for="id" class="text-body-sm">{{ label }}<span class="star">*</span></label>
    <input :type="inputType" :id="id" :name="name" v-model="model" />
  </div>

  <div v-else class="input-group">
    <label :for="id" class="text-body-sm radio-container">
      <input :type="inputType" :id="id" :name="name" :value="value" v-model="model" />
      <span :id="id" class="text-body-sm">{{ label }}</span>
    </label>
  </div>
</template>

<style scoped>
input {
  border: 1px solid var(--color-grey-500);
}

input:hover {
  border-color: var(--color-green-600);
}

/* For any input not a radio or checkbox */
input:not([type='radio'], [type='checkbox']) {
  height: 3rem;
  border-radius: 0.5rem;
}

.input-group:has(input[type='checkbox']) {
  display: flex;
  justify-content: flex-end;
  flex-direction: row-reverse;
  gap: 1rem;
}

.input-group:has(input[type='radio']) label {
  border: 1px solid var(--color-grey-500);
  width: 100%;

  &:hover {
    border-color: var(--color-green-600);
  }
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
