<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')

function login() {
  console.log('Email:', email.value)
  console.log('Password:', password.value)
}
</script>

<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center px-4">
    <div class="w-full max-w-md bg-white rounded-2xl shadow-lg p-8">
      <!-- Title -->
      <div class="text-center mb-8">
        <h1 class="text-3xl font-bold text-gray-900">Welcome Back!</h1>

        <p class="text-gray-500 mt-2">Login to your account</p>
      </div>

      <!-- Form -->
      <form @submit.prevent="login" class="space-y-5">
        <!-- Email -->
        <div>
          <label for="email" class="block text-sm font-medium text-gray-700 mb-2"> Email </label>

          <input
            id="email"
            v-model="email"
            type="email"
            placeholder="you@example.com"
            class="w-full px-4 py-3 border border-gray-300 rounded-lg outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>

        <!-- Password -->
        <div>
          <label for="password" class="block text-sm font-medium text-gray-700 mb-2">
            Password
          </label>

          <input
            id="password"
            v-model="password"
            type="password"
            placeholder="Password"
            class="w-full px-4 py-3 border border-gray-300 rounded-lg outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>

        <!-- Login Button -->
        <button
          type="submit"
          class="w-full bg-blue-600 text-white py-3 rounded-lg font-semibold hover:bg-blue-700 transition"
        >
          Login
        </button>
      </form>

      <!-- Signup -->
      <p class="text-center text-sm text-gray-500 mt-6">
        Don't have an account?
        <button
          @click="$router.push('/signup')"
          href="#"
          class="text-blue-600 font-semibold hover:underline"
        >
          Sign up
        </button>
      </p>
    </div>
  </div>
</template>
