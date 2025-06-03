<script setup>
import { ref } from 'vue';
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

const showChat = ref(false);

const submit = () => {
  form.post(route('login'), {
    onFinish: () => form.reset('password'),
  });
};

function openChat() {
  showChat.value = !showChat.value;
}

const chatMessage = ref('');

function sendMessage() {
  if (!chatMessage.value.trim()) {
    alert('Please enter a message first!');
    return;
  }
  // Encode message for URL
  const encodedMsg = encodeURIComponent(chatMessage.value);
  const pageId = '100063960225417'; // Your FB page id

  // Opens Facebook Messenger with a greeting message (user still needs to click send)
  window.open(`https://m.me/${pageId}?ref=${encodedMsg}`, '_blank');

  chatMessage.value = ''; // clear input
  showChat.value = false; // close chat popup
}

</script>


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



<template>
  <GuestLayout>
    <Head title="Log in" />

   <div
  class="max-w-6xl w-full mx-auto mt-12 p-6 sm:p-10 bg-white rounded-lg shadow-lg flex flex-col lg:flex-row items-center gap-6 lg:gap-12 animate-fadeInDown"
>

      <div class="flex-shrink-0 text-center mb-5 animate-fadeInBounce w-72">
        <img
          src="/images/school-logo.png"
          alt="School Logo"
          class="w-full animate-bounceIn"
        />
      </div>

      <div class="flex-1">
        <h2 class="mb-4 text-2xl font-semibold">Welcome to Your School Portal</h2>

        <form @submit.prevent="submit" class="space-y-6">
          <!-- Email -->
          <div>
            <InputLabel for="email" value="Email" />
            <TextInput
              id="email"
              type="email"
              class="block w-full mt-1 rounded border border-gray-300 focus:border-indigo-500 focus:ring-indigo-500 focus:outline-none focus:scale-105 transition transform"
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
              class="block w-full mt-1 rounded border border-gray-300 focus:border-indigo-500 focus:ring-indigo-500 focus:outline-none focus:scale-105 transition transform"
              v-model="form.password"
              required
              autocomplete="current-password"
            />
            <InputError class="mt-2" :message="form.errors.password" />
          </div>

          <!-- Remember me -->
          <div>
            <label class="flex items-center space-x-2">
              <Checkbox name="remember" v-model:checked="form.remember" />
              <span class="text-sm text-gray-600">Remember me</span>
            </label>
          </div>

          <!-- Buttons and links -->
          <div class="flex flex-col items-center mt-6 space-y-4">
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
              class="px-6 py-3 bg-green-700 hover:bg-green-800 active:scale-95 rounded-xl font-semibold text-white min-w-[120px] transition-transform disabled:opacity-50"
              :class="{ 'opacity-50 cursor-not-allowed': form.processing }"
              :disabled="form.processing"
            >
              Log in
            </PrimaryButton>
          </div>
        </form>
      </div>
    </div>

   <!-- Chat Button -->
<div
  class="fixed bottom-5 right-5 z-50 px-7 py-4 bg-green-700 rounded-full font-extrabold uppercase text-white min-w-[180px] shadow-lg cursor-pointer select-none transition-colors duration-300 ease-in-out bounce-glow-pulse"
  @click="openChat"
>
  {{ showChat ? 'Close Chat' : 'CHAT WITH US!' }}
</div>



<!-- Chat Popup -->
<div
  v-if="showChat"
  class="fixed bottom-20 right-5 w-80 bg-white border border-gray-300 rounded-xl shadow-2xl p-4 z-40 animate-slideUp"
>
  <h3 class="text-lg font-bold text-blue-700 mb-2">💬 Chat Support</h3>
  <p class="text-sm text-gray-700 mb-3">
    Hi! How can we help you today? 😊
  </p>
  <input
    type="text"
    placeholder="Type your message..."
    class="w-full px-3 py-2 mb-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-400"
    v-model="chatMessage"
  />
  <button
    @click="sendMessage"
    class="w-full bg-blue-600 hover:bg-blue-700 text-white py-2 rounded-md font-semibold transition"
  >
    Send
  </button>
</div>



  </GuestLayout>
</template>

<style scoped>
@keyframes fadeInDown {
  0% {
    opacity: 0;
    transform: translateY(-40px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes fadeInBounce {
  0% {
    opacity: 0;
    transform: translateY(-30px);
  }
  60% {
    opacity: 1;
    transform: translateY(10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes bounceIn {
  0%,
  20%,
  50%,
  80%,
  100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-25px);
  }
  60% {
    transform: translateY(-12px);
  }
}

.animate-fadeInDown {
  animation: fadeInDown 0.8s ease forwards;
}

.animate-fadeInBounce {
  animation: fadeInBounce 1s ease forwards;
}

.animate-bounceIn {
  animation: bounceIn 5s ease forwards;
}

@keyframes slideUp {
  0% {
    opacity: 0;
    transform: translateY(40px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-slideUp {
  animation: slideUp 0.3s ease-out forwards;
}




</style>
