<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: Boolean,
    canRegister: Boolean,
    status: String,
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        <div class="flex items-center gap-8 login-wrapper">
  <div class="flex-shrink-0 logo-container">
    <img
      src="/images/school-logo.png"
      alt="School Logo"
      class="logo"
      :class="{ 'logo-spin': typing }"
    />
  </div>

  <div class="flex-1 form-container">
    <h2 class="mb-4">Welcome to Your School Portal</h2>

    <form @submit.prevent="submit" class="space-y-4 login-form">
      <!-- Email -->
      <div>
        <InputLabel for="email" value="Email" />
        <TextInput
          id="email"
          type="email"
          class="block w-full mt-1 input-animated"
          v-model="form.email"
          required
          autofocus
          autocomplete="username"
        />
        <InputError class="mt-2" :message="form.errors.email" />
      </div>

      <!-- Password -->
      <div>
        <InputLabel for="password" value="Password" />
        <TextInput
          id="password"
          type="password"
          class="block w-full mt-1 input-animated"
          v-model="form.password"
          required
          autocomplete="current-password"
        />
        <InputError class="mt-2" :message="form.errors.password" />
      </div>

      <!-- Remember me -->
      <div>
        <label class="flex items-center">
          <Checkbox name="remember" v-model:checked="form.remember" />
          <span class="text-sm text-gray-600 ms-2">Remember me</span>
        </label>
      </div>

      <!-- Buttons and links -->
      <div class="flex flex-col items-center justify-center mt-6 space-y-3">
        <Link
          v-if="canResetPassword"
          :href="route('password.request')"
          class="text-sm text-gray-600 underline hover:text-gray-900"
        >
          Forgot your password?
        </Link>

        <Link
          v-if="canRegister"
          :href="route('register')"
          class="text-sm text-gray-600 underline hover:text-gray-900"
        >
          Register
        </Link>

        <PrimaryButton
          class="login-btn"
          :class="{ 'opacity-25': form.processing }"
          :disabled="form.processing"
        >
          Log in
        </PrimaryButton>
      </div>
    </form>
  </div>
</div>

    </GuestLayout>
</template>
