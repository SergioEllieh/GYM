<script setup>
import { ref } from 'vue'

const name = ref('')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')

function signup() {
  if (password.value !== confirmPassword.value) {
    alert('Passwords does not match!')
    return
  }

  console.log('Name:', name.value)
  console.log('Email:', email.value)
  console.log('Password:', password.value)

  alert('Account created successfully!')
}
</script>

<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="bg-white p-8 rounded-xl shadow-md w-96">
      <h1 class="text-2xl font-bold mb-6">Create Account</h1>

      <form @submit.prevent="signup">
        <!-- Name -->
        <input
          v-model="name"
          type="text"
          placeholder="Full Name"
          required
          class="w-full border p-3 rounded mb-4"
        />

        <!-- Email -->
        <input
          v-model="email"
          type="email"
          placeholder="Email"
          required
          class="w-full border p-3 rounded mb-4"
        />

        <!-- Password -->
        <input
          v-model="password"
          type="password"
          placeholder="Password"
          required
          class="w-full border p-3 rounded mb-4"
        />

        <!-- Confirm Password -->
        <input
          v-model="confirmPassword"
          type="password"
          placeholder="Confirm Password"
          required
          class="w-full border p-3 rounded mb-4"
        />

        <button type="submit" class="w-full bg-blue-600 text-white p-3 rounded">Sign Up</button>
      </form>

      <p class="text-center mt-5">
        Already have an account?

        <router-link :to="{name: 'login'}" class="text-blue-600 font-semibold"> Login </router-link>
      </p>
    </div>
  </div>
</template>
