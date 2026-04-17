<script setup>
defineProps({
  label: {
    type: String,
  },
  error: {
    type: String,
  },
  errorId: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <div :id="errorId">
    <template v-if="error">
      <span v-if="!!label" class="visually-hidden">{{ label }} error</span>
      <span class="error-text text-body-md-regular">{{ error }}</span>
    </template>
  </div>
</template>

<style scoped>
.visually-hidden {
  /* Shrink the element to a single pixel */
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;

  overflow: hidden;

  /* Clip the element so it has no visible area */
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;

  border: 0;
}
</style>
