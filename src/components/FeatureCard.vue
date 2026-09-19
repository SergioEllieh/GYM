<script setup>
defineProps({
  title: String,
  description: String,
  icon: String,
})
</script>

<template>
  <div
    class="rounded-2xl text-center bg-gray-100 p-8 transition hover:-translate-y-2 hover:shadow-2xl"
  >
    <div class="mb-5 text-3xl">
      {{ icon }}
    </div>
    <h3 class="text-xl font-bold text-gray-900">
      {{ title }}
    </h3>

    <p class="mt-3 text-gray-600">
      {{ description }}
    </p>
  </div>
</template>
