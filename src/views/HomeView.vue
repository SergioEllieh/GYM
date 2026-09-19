<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

import FeatureCard from '../components/FeatureCard.vue'
import ProgramCard from '../components/ProgramCard.vue'
import BaseModal from '../components/BaseModal.vue'
import MembershipPlans from '../components/MembershipPlans.vue'

const title = "Sergio's GYM"

const router = useRouter()

const isMenuOpen = ref(false)

const selectedProgram = ref(null)

const programs = [
  {
    title: 'Strength Training',
    description: 'Build strength and muscle with structured resistance training.',
    level: 'All Levels',
  },
  {
    title: 'Muscle Building',
    description: 'Focused workouts designed to help you gain muscle mass.',
    level: 'Intermediate',
  },
  {
    title: 'Fat Loss',
    description: 'Combine effective training with conditioning to improve body composition.',
    level: 'All Levels',
  },
  {
    title: 'Personal Training',
    description: 'Get a personalized training approach based on your goals.',
    level: 'All Levels',
  },
]

const plans = [
  {
    name: 'Basic',
    price: 20,
    description: 'For people who want access to the gym.',
    features: ['Gym access', 'Basic equipment', 'Locker access'],
    popular: false,
  },
  {
    name: 'Pro',
    price: 35,
    description: 'For people who want more guidance and benefits.',
    features: [
      'Everything in Basic',
      'Personal training guidance',
      'Workout plan',
      'Progress tracking',
    ],
    popular: true,
  },
  {
    name: 'Elite',
    price: 50,
    description: 'For people who want the complete training experience.',
    features: ['Everything in Pro', 'Personal trainer', 'Nutrition guidance', 'Priority support'],
    popular: false,
  },
]

function handleLearnMore(program) {
  selectedProgram.value = program
}

function handlePlanSelected(plan) {
  router.push({
    path: '/signup',
    query: {
      plan: plan.name,
    },
  })
}
</script>

<template>
  <!--Navbar-->
  <header class="bg-gray-950 text-white">
    <nav class="flex items-center justify-between px-4 py-5 md:px-8">
      <div class="text-2xl font-bold">
        {{ title }}
      </div>
      <div class="hidden md:flex gap-8">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/programs">Programs</RouterLink>
        <RouterLink to="/contact">Contact</RouterLink>
      </div>
      <div class="hidden md:flex gap-8">
        <RouterLink to="/login" class="px-4 py-2">Login</RouterLink>
        <RouterLink to="/signup" class="px-4 py-2">Signup</RouterLink>
      </div>
      <button @click="isMenuOpen = !isMenuOpen" class="md:hidden">☰</button>
    </nav>
    <div v-if="isMenuOpen" class="md:hidden px-4 pb-5">
      <div class="flex flex-col gap-4">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/programs">Programs</RouterLink>
        <RouterLink to="/contact">Contact</RouterLink>

        <RouterLink to="/login"> Login </RouterLink>

        <RouterLink to="/signup"> Signup </RouterLink>
      </div>
    </div>
  </header>

  <!--Hero-->
  <section class="min-h-[80vh] bg-gray-900 text-white flex items-center justify-center px-4">
    <div class="max-w-3xl text-center">
      <p class="mb-4 text-sm uppercase tracking-widest text-gray-400">Train. Improve. Repeat.</p>

      <h1 class="text-4xl font-bold md:text-6xl">Build Your Strongest Self</h1>

      <p class="mx-auto mt-6 max-w-xl text-lg text-gray-300">
        Train with purpose, become stronger, and reach your fitness goals.
      </p>

      <RouterLink
        to="/signup"
        class="mt-8 inline-block rounded-lg bg-white px-8 py-4 font-semibold text-black hover:bg-gray-300 transition"
      >
        Start Training
      </RouterLink>
    </div>
  </section>

  <!--Feature Card-->
  <section class="bg-white px-4 py-20">
    <div class="mx-auto max-w-6xl">
      <p class="text-center text-sm font-semibold uppercase tracking-widest text-gray-500">
        Why Sergio's GYM
      </p>

      <h2 class="mt-3 text-center text-3xl font-bold text-gray-900 md:text-4xl">
        Everything You Need To Get Stronger
      </h2>

      <div class="mt-12 grid gap-6 md:grid-cols-3">
        <FeatureCard
          icon="🏋️"
          title="Expert Trainers"
          description="Learn from experienced trainers who help you reach your goals."
        />

        <FeatureCard
          icon="💪"
          title="Modern Equipment"
          description="Train with quality equipment designed for effective workouts."
        />

        <FeatureCard
          icon="⚡"
          title="Personal Training"
          description="Get guidance and a training approach built around your goals."
        />
      </div>
    </div>
  </section>

  <!--Programs-->
  <section class="bg-gray-950 px-4 py-20 text-white">
    <div class="mx-auto max-w-6xl">
      <p class="text-center text-sm font-semibold uppercase tracking-widest text-gray-400">
        Our Programs
      </p>

      <h2 class="mt-3 text-center text-3xl font-bold md:text-4xl">Choose Your Training</h2>

      <div class="mt-12 grid gap-6 md:grid-cols-2">
        <ProgramCard
          v-for="program in programs"
          :key="program.title"
          :title="program.title"
          :description="program.description"
          :level="program.level"
          @learn-more="handleLearnMore(program)"
        />
      </div>
    </div>
    <BaseModal :open="selectedProgram !== null" @close="selectedProgram = null">
      <div class="flex items-center justify-between">
        <h3 class="text-2xl font-bold">{{ selectedProgram.title }}</h3>
        <button @click="selectedProgram = null" class="text-2xl text-gray-500 hover:text-gray-900">
          ×
        </button>
      </div>
      <p class="mt-6 text-gray-600">
        {{ selectedProgram.description }}
      </p>

      <p class="mt-4 font-semibold">Level: {{ selectedProgram.level }}</p>
      <div class="mt-6 flex justify-end">
        <button
          @click="selectedProgram = null"
          class="rounded-lg bg-gray-900 px-6 py-3 font-semibold text-white transition hover:bg-gray-700"
        >
          Close
        </button>
      </div>
    </BaseModal>
  </section>

  <!--Plans-->
  <MembershipPlans :plans="plans" @plan-selected="handlePlanSelected" />
</template>
