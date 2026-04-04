<script setup>
import { ref } from 'vue'
import FormInput from './components/FormInput.vue'

const firstName = ref('')
const lastName = ref('')
const email = ref('')
const queryType = ref('')
const message = ref('')
const consent = ref(false)
</script>

<template>
  <form>
    <h1 class="text-heading">Contact Us</h1>
    <div class="form-group">
      <FormInput label="First Name" id="first-name" v-model="firstName" />
      <FormInput label="Last Name" id="last-name" v-model="lastName" />
    </div>
    <div class="form-group">
      <FormInput label="Email" id="email" v-model="email" />
    </div>
    <fieldset class="form-group">
      <legend class="text-body-sm">Query Type<span class="star">*</span></legend>
      <div class="input-group">
        <FormInput
          label="General Enquiry"
          id="general-enquiry"
          input-type="radio"
          name="query-type"
          value="general-enquiry"
          v-model="queryType"
        />
        <FormInput
          label="Support Request"
          id="support-request"
          input-type="radio"
          name="query-type"
          value="support-request"
          v-model="queryType"
        />
      </div>
    </fieldset>

    <div class="form-group">
      <div class="input-group">
        <label for="message" class="text-body-sm">Message<span class="star">*</span></label>
        <textarea name="message" rows="8" id="message" v-model="message"></textarea>
      </div>
    </div>

    <div class="form-group">
      <FormInput
        label="I consent to being contacted by the team"
        id="consent"
        input-type="checkbox"
        v-model="consent"
      />
    </div>
    <button type="submit" class="text-body-sm">Submit</button>
  </form>
</template>

<style scoped>
h1 {
  color: var(--color-grey-900);
}

form {
  background-color: var(--color-white);
  width: 100%;
  border-radius: 1rem;
  padding: 2.5rem;
  max-width: 46rem;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.input-group:has(textarea) {
  gap: 0.5rem;
}

.input-group:has(input[type='radio']) {
  gap: 1rem;
  display: flex;
  flex: 1;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

fieldset {
  border: none;
}

legend {
  margin-bottom: 1rem;
  color: var(--color-grey-900);
}

textarea {
  border-radius: 0.5rem;
  font-family: 'Karla', sans-serif;
  padding: 0.5rem;
  border: 1px solid var(--color-grey-500);

  &:hover {
    border-color: var(--color-green-600);
  }
}

button {
  width: 100%;
  height: 3.5rem;
  color: var(--color-white);
  background-color: var(--color-green-600);
  border: none;
  border-radius: 0.5rem;

  &:hover {
    background-color: color-mix(in srgb, var(--color-green-600), black 50%);
  }
}

@media (min-width: 48rem) {
  .form-group:not(:has(textarea)) {
    display: flex;
    flex-direction: row;
  }

  .form-group > * {
    flex: 1;
  }

  .input-group:has(input[type='radio']) {
    flex-direction: row;
  }
}
</style>

<style>
.star {
  margin-left: 0.5rem;
  color: var(--color-green-600);
}

label {
  color: var(--color-grey-900);
}
</style>
