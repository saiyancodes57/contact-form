<script setup></script>

<template>
  <div class="shared-container">
    <slot></slot>
  </div>
</template>

<style scoped>
.shared-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

@media (min-width: 48rem) {
  .shared-container {
    display: flex;
    flex-direction: row;
    gap: 1rem;
  }
}
</style>
