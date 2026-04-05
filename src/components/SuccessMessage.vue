<script setup>
import IconSuccess from '@/images/icon-success-check.svg'

// Define the prop coming from the parent
defineProps({
  show: Boolean,
})
</script>

<template>
  <Transition name="toast">
    <div v-if="show" class="message-sent">
      <div class="top">
        <img :src="IconSuccess" alt="" />
        <p class="text-body-sm">Message Sent</p>
      </div>
      <p class="text-body-sm">Thanks for completing the form. We'll be in touch soon!</p>
    </div>
  </Transition>
</template>

<style scoped>
.top {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
  align-items: center;
}

/* 1. Base Class: Set the "Resting" state */
.message-sent {
  position: fixed;
  top: 20px;
  left: 50%;
  /* CRITICAL: Must be exactly the same as the 'enter-to' state */
  transform: translateX(-50%);

  z-index: 1000;
  width: 95%;
  max-width: 28rem;
  background-color: var(--color-grey-900);
  color: var(--color-white);
  padding: 2rem;
  border-radius: 0.5rem;
}

/* 2. Starting/Ending states (The "Hidden" positions) */
.toast-enter-from,
.toast-leave-to {
  /* We keep the -50% for the X axis, but change the Y axis */
  transform: translate(-50%, -100%);
  opacity: 0;
}

/* 3. The "Target" states (The "Visible" positions) */
.toast-enter-to,
.toast-leave-from {
  /* This MUST match the base class horizontal centering */
  transform: translate(-50%, 0);
  opacity: 1;
}

/* 4. The Timing */
.toast-enter-active,
.toast-leave-active {
  transition:
    transform 0.5s ease,
    opacity 0.5s ease;
}
</style>
