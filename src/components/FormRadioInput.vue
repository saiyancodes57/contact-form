<script setup>
defineEmits(['blur-event'])
const model = defineModel()
defineProps({
  labelText: {
    type: String,
    required: true,
  },
  value: {
    type: String,
    required: true,
  },
  name: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <label class="text-body-sm">
    <input type="radio" :value="value" :name="name" v-model="model" @blur="$emit('blur-event')" />
    {{ labelText }}
  </label>
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
