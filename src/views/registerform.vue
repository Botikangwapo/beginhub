<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { registerUser } from '../services/authuserservices.js';

const router = useRouter()

const firstname = ref('')
const lastname = ref('')
const email = ref('')
const password = ref('')

const errorMessage = ref('')
const successMessage = ref('')
const isLoading = ref(false)

const showPassword = ref(false);

const togglePassword = () => {
    showPassword.value = !showPassword.value;
};

const handleRegister = async () => {
    errorMessage.value = ''
    successMessage.value = ''
    isLoading.value = true

    const result = await registerUser(email.value, password.value, firstname.value, lastname.value)

    if (result.success) {
        successMessage.value = "Nice! Registered ka na bossing! Welcome sa BeginHub."

        firstname.value = ''
        lastname.value = ''
        email.value = ''
        password.value = ''

        setTimeout(() => {
            router.push('/Verification')
        }, 2000)
    } else {
        errorMessage.value = result.error || 'May nagka-error sa pag-register bossing.'
        isLoading.value = false
    }
}
</script>
<template>
    <section class="grid grid-cols-1 2xl:grid-cols-2 min-h-screen bg-blue-50/20">
        <div class="hidden 2xl:flex flex-col justify-between bg-blue-600 p-12 text-white">
            <h1 class="text-3xl font-black tracking-tighter uppercase">Storage.Repo</h1>
            <div class="space-y-4">
                <h2 class="text-5xl font-black leading-tight uppercase">Begin<span class="text-blue-200">Hub</span></h2>
                <p class="text-blue-100 font-bold tracking-wide">Register to initialize your <br> execution environment.
                </p>
            </div>
            <div class="text-[10px] font-black uppercase tracking-widest opacity-60">WHITE & BLUE // AUTH_SERVICE_V5
            </div>
        </div>

        <div class="flex items-center justify-center p-6 min-h-screen bg-gray-50">
            <form @submit.prevent="handleRegister"
                class="w-full max-w-md bg-white p-8 rounded-2xl border border-gray-200 shadow-sm space-y-6">

                <div class="space-y-1">
                    <router-link to="/" class="text-sm text-blue-600 hover:text-blue-800 flex items-center gap-1 mb-4">
                        &larr; Back to Home
                    </router-link>
                    <h1 class="text-2xl font-bold text-blue-900">Create an account</h1>
                    <p class="text-sm text-gray-500">Sign up to get started with your profile.</p>
                </div>

                <div v-if="errorMessage" class="p-4 text-sm text-red-700 bg-red-50 border border-red-200 rounded-lg">
                    {{ errorMessage }}
                </div>
                <div v-if="successMessage"
                    class="p-4 text-sm text-emerald-700 bg-emerald-50 border border-emerald-200 rounded-lg">
                    {{ successMessage }}
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div class="flex flex-col gap-1.5">
                        <label class="text-sm font-medium text-gray-700">First Name</label>
                        <input v-model="firstname" type="text" placeholder="John" required
                            class="w-full p-3 rounded-xl border border-gray-300 focus:ring-2 focus:ring-blue-500 outline-none transition">
                    </div>
                    <div class="flex flex-col gap-1.5">
                        <label class="text-sm font-medium text-gray-700">Last Name</label>
                        <input v-model="lastname" type="text" placeholder="Doe" required
                            class="w-full p-3 rounded-xl border border-gray-300 focus:ring-2 focus:ring-blue-500 outline-none transition">
                    </div>
                </div>

                <div class="flex flex-col gap-1.5">
                    <label class="text-sm font-medium text-gray-700">Email Address</label>
                    <input v-model="email" type="email" placeholder="name@example.com" required
                        class="w-full p-3 rounded-xl border border-gray-300 focus:ring-2 focus:ring-blue-500 outline-none transition">
                </div>

                <div class="flex flex-col gap-1.5">
                    <label class="text-sm font-medium text-gray-700">Password</label>

                    <div class="flex justify-between items-center relative">
                        <input v-model="password" :type="showPassword ? 'text' : 'password'" placeholder="••••••••"
                            required
                            class="w-full p-3 rounded-xl border border-gray-300 focus:ring-2 focus:ring-blue-500 outline-none transition">
                        <button type="button" @click="togglePassword"
                            class="absolute right-5 text-xs text-blue-600 hover:underline">
                            {{ showPassword ? 'Hide' : 'Show' }}
                        </button>
                    </div>

                </div>

                <label class="flex items-center gap-2 cursor-pointer">
                    <input type="checkbox" class="w-4 h-4 rounded border-gray-300 text-blue-600 focus:ring-blue-500"
                        required>
                    <span class="text-sm text-gray-600">I agree to the <a href="#"
                            class="text-blue-600 font-medium hover:underline">Terms & Policy</a></span>
                </label>

                <button :disabled="isLoading" type="submit"
                    class="w-full py-3 rounded-xl bg-blue-600 text-white font-semibold hover:bg-blue-700 transition disabled:bg-blue-400">
                    {{ isLoading ? 'Registering...' : 'Create Account' }}
                </button>

                <p class="text-center text-sm text-gray-600">
                    Already have an account?
                    <router-link to="/login" class="text-blue-600 font-semibold hover:underline">Login
                        here</router-link>
                </p>
            </form>
        </div>
    </section>
</template>