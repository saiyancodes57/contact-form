<script setup>
import { ref, computed } from 'vue'
import errorMessages from '@/errorMessages.json'

const model = defineModel()
defineEmits(['blur-emit'])
const props = defineProps({
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

const hasError = ref(false)
function validate() {
  // Checks that the consent checkbox has been clicked
  if (props.inputType === 'checkbox') {
    hasError.value = model.value !== true
    return
  }

  // Only use trim() when not a false/true value, as it would throw an error
  const val = model.value?.trim()

  if (props.inputType === 'text') {
    hasError.value = val === ''
    return
  }

  if (props.inputType === 'email') {
    hasError.value = val === '' || !val.includes('@')
    return
  }

  if (props.inputType === 'radio') {
    const validOptions = ['general-enquiry', 'support-request']
    hasError.value = !validOptions.includes(val)
    return
  }
}

const errorMessage = computed(() => {
  return errorMessages[props.inputType]
})

const selectedRadio = computed(() => {
  return model.value === props.value
})
</script>

<template>
  <div v-if="inputType === 'checkbox'" class="input-group">
    <div class="checkbox-wrapper">
      <label :for="id" class="text-body-sm">{{ label }}<span class="star">*</span></label>
      <input
        :type="inputType"
        :id="id"
        :name="name"
        :class="{ error: hasError }"
        v-model="model"
        required
        @blur="validate"
      />
    </div>
    <p v-if="hasError" class="text-body-sm error-text">{{ errorMessage }}</p>
  </div>

  <div v-else-if="inputType !== 'radio'" class="input-group">
    <label :for="id" class="text-body-sm">{{ label }}<span class="star">*</span></label>
    <input
      :type="inputType"
      :id="id"
      :name="name"
      :class="{ error: hasError }"
      v-model="model"
      required
      @blur="validate"
    />
    <p v-if="hasError" class="text-body-sm error-text">{{ errorMessage }}</p>
  </div>

  <div v-else class="input-group">
    <label :for="id" class="text-body-sm radio-container" :class="{ selected: selectedRadio }">
      <input
        :type="inputType"
        :id="id"
        :name="name"
        :value="value"
        v-model="model"
        @blur="$emit('blur-emit')"
        required
      />
      <span :id="id" class="text-body-sm">{{ label }}</span>
    </label>
  </div>
</template>

<style scoped>
.error {
  border: 1px solid var(--color-red-errors);
}

.error-text {
  color: var(--color-red-errors);
}

input {
  border: 1px solid var(--color-grey-500);
  padding: 0.5rem;
}

input:hover {
  border-color: var(--color-green-600);
}

/* For any input not a radio or checkbox */
input:not([type='radio'], [type='checkbox']) {
  height: 3rem;
  border-radius: 0.5rem;
}

.checkbox-wrapper:has(input[type='checkbox']) {
  display: flex;
  justify-content: flex-end;
  flex-direction: row-reverse;
  gap: 1rem;
}

.input-group:has(input[type='radio']) label {
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

.radio-container.selected {
  background-color: var(--color-green-200);
  border-color: var(--color-green-600);
}

.radio-container.selected:has(input[type='radio']) {
  accent-color: var(--color-green-600);
}
</style>
