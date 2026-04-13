<script setup>
defineProps({
  label: {
    type: String,
    required: true,
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
      <span class="visually-hidden">{{ label }} error</span>
      <span class="error-text">{{ error }}</span>
    </template>
  </div>
</template>

<style scoped>
.visually-hidden {
  /* 1. Shrink the element to a single pixel */
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;

  /* 2. Hide any overflow */
  overflow: hidden;

  /* 3. Clip the element so it has no visible area */
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;

  /* 4. Remove borders */
  border: 0;
}
</style>
