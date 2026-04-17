<script setup>
import IconSuccess from '@/images/icon-success-check.svg'

defineProps({
  show: Boolean,
})
</script>

<template>
  <div class="toast-wrapper" aria-live="polite" role="status">
    <Transition name="toast">
      <div v-if="show" class="message-sent">
        <div class="top">
          <img :src="IconSuccess" alt="" />
          <p class="text-body-md-regular">Message Sent</p>
        </div>
        <p class="text-body-md-regular">Thanks for completing the form. We'll be in touch soon!</p>
      </div>
    </Transition>
  </div>
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
