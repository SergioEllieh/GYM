<script setup>
import { onMounted, onUnmounted } from 'vue'

defineProps({
  open: Boolean,
})

const emit = defineEmits(['close'])

function handleEscape(event) {
  if (event.key === 'Escape') {
    emit('close')
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleEscape)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleEscape)
})
</script>

<template>
  <Transition name="modal">
    <div
      v-if="open"
      @click="emit('close')"
      class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 px-4"
    >
      <div
        @click.stop
        class="modal-box w-full max-w-lg rounded-2xl bg-white p-8 text-gray-900"
      >
        <slot />
      </div>
    </div>
  </Transition>
</template>

<style>
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-box {
  transition: transform 0.5s ease;
}

.modal-enter-from .modal-box,
.modal-leave-to .modal-box {
  transform: scale(0.95);
}
</style>
