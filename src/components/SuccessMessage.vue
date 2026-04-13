<script setup>
import IconSuccess from '@/images/icon-success-check.svg'

defineProps({
  show: Boolean,
})
</script>

<template>
  <Transition name="toast">
    <div v-if="show" class="message-sent" aria-live="polite">
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

.message-sent {
  position: fixed;
  top: 20px;
  left: 50%;

  transform: translateX(-50%);

  z-index: 1000;
  width: 95%;
  max-width: 28rem;
  background-color: var(--color-grey-900);
  color: var(--color-white);
  padding: 2rem;
  border-radius: 0.5rem;
}

.toast-enter-from,
.toast-leave-to {
  transform: translate(-50%, -100%);
  opacity: 0;
}

.toast-enter-to,
.toast-leave-from {
  transform: translate(-50%, 0);
  opacity: 1;
}

.toast-enter-active,
.toast-leave-active {
  transition:
    transform 0.5s ease,
    opacity 0.5s ease;
}
</style>
