<script setup>
import { ref, watch, useTemplateRef } from 'vue'
import errorMessages from '@/errorMessages.json'
import SuccessMessage from './components/SuccessMessage.vue'
import SharedContainerSlot from './components/SharedContainerSlot.vue'
import BaseFormInput from './components/BaseFormInput.vue'
import FormRadioInput from './components/FormRadioInput.vue'
import TextAreaComp from './components/TextAreaComp.vue'
import FormCheckbox from './components/FormCheckbox.vue'

const form = ref({
  firstName: '',
  lastName: '',
  email: '',
  queryType: '',
  message: '',
  consent: false,
})

// Return true if valid, return error if invalid
const validators = {
  firstName: (val) => val.trim() !== '' || errorMessages.firstName,
  lastName: (val) => val.trim() !== '' || errorMessages.lastName,
  email: (val) => (val.trim() !== '' && val.includes('@')) || errorMessages.email,
  queryType: (val) =>
    ['general-enquiry', 'support-request'].includes(val) || errorMessages.queryType,
  message: (val) => val.trim() !== '' || errorMessages.message,
  consent: (val) => val === true || errorMessages.consent,
}

const errors = ref({
  firstName: '',
  lastName: '',
  email: '',
  queryType: '',
  message: '',
  consent: '',
})

const queryOptions = [
  { value: 'general-enquiry', label: 'General Enquiry' },
  { value: 'support-request', label: 'Support Request' },
]

watch(
  form,
  () => {
    for (const field in errors.value) {
      if (errors.value[field]) validate(field)
    }
  },
  { deep: true },
)

// Vue template ref definitions
const firstNameRef = useTemplateRef('first-name')
const lastNameRef = useTemplateRef('last-name')
const emailRef = useTemplateRef('email')
const queryTypeRef = useTemplateRef('query-type')
const messageRef = useTemplateRef('message')
const consentRef = useTemplateRef('consent')

// Order of form fields
const formOrder = ['firstName', 'lastName', 'email', 'queryType', 'message', 'consent']

// Maps form fields to corresponding vue template refs
const orderRefMapping = {
  firstName: firstNameRef,
  lastName: lastNameRef,
  email: emailRef,
  queryType: queryTypeRef,
  message: messageRef,
  consent: consentRef,
}

// Takes a specific field and uses the validator function to return true OR empty string
function validate(field) {
  const result = validators[field](form.value[field])
  errors.value[field] = result === true ? '' : result
}

// Handling form submission
function handleSubmit() {
  let isValid = true
  // Validate each form field
  for (const field of Object.keys(form.value)) {
    validate(field)
    // If error object contains error - form invalid
    if (errors.value[field]) {
      isValid = false
    }
  }

  if (isValid) {
    console.log('Form is ready to be submitted')
    showToast.value = true
    setTimeout(() => {
      showToast.value = false
    }, 5000)
  } else {
    // When not valid - go through form in order, find 1st error and focus() it.
    for (const field of formOrder) {
      if (errors.value[field]) {
        orderRefMapping[field]?.value.focusInput()
        break
      }
    }
    console.log('Submission blocked: errors still exist.')
  }
  // Do we need a return here? Not necessary I think!?
  // return isValid
}

// Ref for showing toast
const showToast = ref(false)
</script>

<template>
  <SuccessMessage :show="showToast" />
  <main>
    <h1 class="text-heading">Contact Us</h1>
    <form @submit.prevent="handleSubmit" novalidate>
      <SharedContainerSlot>
        <BaseFormInput
          label="First Name"
          type="text"
          autocomplete="given-name"
          v-model="form.firstName"
          :error="errors.firstName"
          @blur-event="validate('firstName')"
          ref="first-name"
        />
        <BaseFormInput
          label="Last Name"
          type="text"
          autocomplete="family-name"
          v-model="form.lastName"
          :error="errors.lastName"
          @blur-event="validate('lastName')"
          ref="last-name"
        />
      </SharedContainerSlot>
      <BaseFormInput
        label="Email"
        type="email"
        autocomplete="email"
        v-model="form.email"
        :error="errors.email"
        @blur-event="validate('email')"
        ref="email"
      />
      <FormRadioInput
        legend="Query Type"
        name="query-type"
        :options="queryOptions"
        v-model="form.queryType"
        :error="errors.queryType"
        @blur-event="validate('queryType')"
        ref="query-type"
      />
      <TextAreaComp
        label="Message"
        v-model="form.message"
        :error="errors.message"
        @blur-event="validate('message')"
        ref="message"
      />
      <FormCheckbox
        name="consent"
        label="I consent to being contacted by the team"
        v-model="form.consent"
        :error="errors.consent"
        @blur-event="validate('consent')"
        ref="consent"
      />
      <button type="submit" class="text-body-sm">Submit</button>
    </form>
  </main>
</template>

<style scoped>
h1 {
  color: var(--color-grey-900);
  margin-bottom: 2rem;
}

main {
  background-color: var(--color-white);
  width: 100%;
  border-radius: 1rem;
  padding: 2.5rem;
  max-width: 46rem;
}

fieldset {
  border: none;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

button {
  width: 100%;
  height: 3.5rem;
  color: var(--color-white);
  background-color: var(--color-green-600);
  border: none;
  border-radius: 0.5rem;
  outline-offset: 3px;

  &:hover {
    background-color: color-mix(in srgb, var(--color-green-600), black 50%);
  }
}
</style>

<style>
input {
  border-radius: 0.5rem;
  height: 3rem;
  border: 1px solid var(--color-grey-500);
}

div:has(input[type='text'], input[type='email'], textarea) label {
  margin-bottom: 0.5rem;
}

.error-text {
  color: var(--color-red-errors);
  font-family: Karla;
  margin-top: 0.5rem;
}
.star {
  margin-left: 0.5rem;
  color: var(--color-green-600);
}

label {
  color: var(--color-grey-900);
}
</style>
