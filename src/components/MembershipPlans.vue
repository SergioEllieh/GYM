<script setup>
import { ref } from 'vue'
import BaseModal from './BaseModal.vue'

defineProps({
  plans: {
    type: Array,
    required: true,
  },
})
const emit = defineEmits(['plan-selected'])

const selectedPlan = ref(null)
const confirmedPlan = ref(null)
const isConfirmed = ref(false)

function choosePlan(plan) {
  selectedPlan.value = plan
}

function confirmPlan() {
  const plan = selectedPlan.value

  confirmedPlan.value = plan
  emit('plan-selected', plan)

  selectedPlan.value = null
  isConfirmed.value = true
}
</script>

<template>
  <section class="bg-white px-4 py-20">
    <div class="mx-auto max-w-6xl">
      <p class="text-center text-sm font-semibold uppercase tracking-widest text-gray-500">
        Membership
      </p>

      <h2 class="mt-3 text-center text-3xl font-bold text-gray-900 md:text-4xl">
        Choose Your Plan
      </h2>
      <div class="mt-12 grid gap-6 md:grid-cols-3">
        <div
          v-for="plan in plans"
          :key="plan.name"
          :class="[
            'flex h-full flex-col rounded-2xl p-8 text-center',
            plan.popular ? 'border-2 border-black shadow-xl scale-105' : 'border border-gray-200',
          ]"
        >
          <p
            v-if="plan.popular"
            class="mb-3 text-sm font-bold uppercase tracking-widest text-gray-900"
          >
            Most Popular
          </p>
          <h3 class="text-2xl font-bold text-gray-900">
            {{ plan.name }}
          </h3>

          <p class="mt-4 text-4xl font-bold text-gray-900">${{ plan.price }}</p>

          <p class="mt-4 text-gray-600">
            {{ plan.description }}
          </p>
          <ul class="mt-6 space-y-3 text-left">
            <li v-for="feature in plan.features" :key="feature" class="text-gray-700">
              ✓ {{ feature }}
            </li>
          </ul>
          <button
            @click="choosePlan(plan)"
            class="mt-auto w-full rounded-lg bg-gray-900 px-6 py-3 font-semibold text-white transition hover:bg-gray-700"
          >
            Choose Plan
          </button>
        </div>
      </div>

      <!--BaseModal 1-->
      <BaseModal :open="selectedPlan !== null" @close="selectedPlan = null">
        <h3 class="text-2xl font-bold">
          {{ selectedPlan.name }}
        </h3>

        <p class="mt-4 text-gray-600">
          {{ selectedPlan.description }}
        </p>

        <p class="mt-4 text-xl font-bold">${{ selectedPlan.price }} / month</p>

        <ul class="mt-6 space-y-2">
          <li v-for="feature in selectedPlan.features" :key="feature" class="text-gray-700">
            ✓ {{ feature }}
          </li>
        </ul>

        <div class="mt-8 flex justify-end">
          <button
            @click="confirmPlan"
            class="rounded-lg bg-gray-900 px-6 py-3 font-semibold text-white transition hover:bg-gray-700"
          >
            Confirm
          </button>
        </div>
      </BaseModal>
      <!--BaseModal 2-->
      <BaseModal :open="isConfirmed" @close="isConfirmed = false">
        <div class="text-center">
          <h3 class="text-2xl font-bold text-gray-900">Plan Selected</h3>

          <p class="mt-4 text-gray-600">
            Your
            <span class="font-semibold text-gray-900">
              {{ confirmedPlan.name }}
            </span>
            plan has been selected successfully.
          </p>

          <p class="mt-3 text-xl font-bold text-gray-900">${{ confirmedPlan.price }} / month</p>

          <button
            @click="isConfirmed = false"
            class="mt-6 rounded-lg bg-gray-900 px-6 py-3 font-semibold text-white transition hover:bg-gray-700"
          >
            Close
          </button>
        </div>
      </BaseModal>
    </div>
  </section>
</template>
