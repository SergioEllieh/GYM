<script setup>
defineProps({
  title: String,
  description: String,
  level: String,
})
const emit = defineEmits(['learn-more'])
</script>

<template>
  <div class="rounded-2xl text-center bg-gray-900 p-8 transition hover:-translate-y-2 hover:shadow-lg">
    <p class="text-sm font-semibold uppercase tracking-widest text-gray-400">
      {{ level }}
    </p>

    <h3 class="mt-3 text-2xl font-bold text-white">
      {{ title }}
    </h3>

    <p class="mt-4 text-gray-400">
      {{ description }}
    </p>

    <!-- <button
      class="mt-6 rounded-lg bg-white px-6 py-3 font-semibold text-black transition hover:bg-gray-200"
    >
      Learn More
    </button> -->
    <button
          @click="emit('learn-more')"
          class="mt-6 rounded-lg bg-white px-6 py-3 font-semibold text-black transition hover:bg-gray-300"
        >
          Learn More
        </button>
  </div>
</template>
