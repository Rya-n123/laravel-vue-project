<template>
    <div class="flex flex-col items-center justify-center min-h-screen p-6 bg-gray-100">
      <h1 class="mb-6 text-4xl font-bold text-blue-600">Welcome to My Laravel Vue App! 😄</h1>

      <p class="mb-4 text-gray-700">Please login or register to continue.</p>

      <div class="space-x-4">
        <Link
          v-if="canLogin"
          href="/login"
          class="px-5 py-2 text-white transition bg-blue-500 rounded hover:bg-blue-600"
        >
          Login
        </Link>

        <Link
          v-if="canRegister"
          href="/register"
          class="px-5 py-2 text-white transition bg-green-500 rounded hover:bg-green-600"
        >
          Register
        </Link>
      </div>

      <footer class="mt-10 text-sm text-gray-500">
        Laravel v{{ laravelVersion }} | PHP v{{ phpVersion }}
      </footer>
    </div>
  </template>

  <script>
  import { Link } from '@inertiajs/inertia-vue3'

  export default {
    components: {
      Link,
    },
    props: {
      canLogin: Boolean,
      canRegister: Boolean,
      laravelVersion: String,
      phpVersion: String,
    },
  }
  </script>

  <style scoped>
  /* Add any extra styling here */
  </style>
