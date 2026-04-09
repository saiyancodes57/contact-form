<script setup>
// import { ref } from 'vue'
defineEmits(['blur-event'])
const model = defineModel()
defineProps({
  labelText: {
    type: String,
    required: true,
  },
  id: {
    type: String,
    required: true,
  },
  inputType: {
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
    <label :for="id" class="text-body-sm">{{ labelText }}<span class="star">*</span></label>
    <input
      :type="inputType"
      :id="id"
      v-model="model"
      :autocomplete="autocomplete"
      @blur="$emit('blur-event')"
      required
    />
    <p class="error-text">{{ error }}</p>
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  flex: 1;
}
</style>
