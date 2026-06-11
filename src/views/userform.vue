<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router'
import { loginUser } from '../services/authuserservices.js'

const router = useRouter()

const email = ref('')
const password = ref('')

const errorMessage = ref('')
const successMessage = ref('')
const isLoading = ref(false)
const showPassword = ref(false);

const togglePassword = () => {
    showPassword.value = !showPassword.value;
};

const handleLogin = async () => {
    errorMessage.value = ''
    successMessage.value = ''
    isLoading.value = true

    const result = await loginUser(email.value, password.value)

    if (result.success) {
        email.value = ''
        password.value = ''

        setTimeout(() => {
            router.push('/Dash')
        }, 1000)
    } else {
        isLoading.value = false

        const rawError = result.error ? result.error.toLowerCase() : ''

        if (rawError.includes('confirmed') || rawError.includes('confirmation')) {
            errorMessage.value = 'Please comfirm verification in your inbox pare ko!'
        } else if (rawError.includes('invalid clones') || rawError.includes('invalid credentials')) {
            errorMessage.value = 'Invalid credentials pre'
        } else {
            // Fallback para sa iba pang random errors (gaya ng internet connection issue)
            errorMessage.value = result.error || 'Error'
        }
    }
}
</script>

<template>
    <section class="grid grid-cols-1 2xl:grid-cols-2 min-h-screen bg-blue-50/20">
        <div class="hidden 2xl:flex flex-col justify-between bg-blue-600 p-12 text-white">
            <h1 class="text-3xl font-black tracking-tighter uppercase">Storage.Repo</h1>
            <div class="space-y-4">
                <h2 class="text-5xl font-black leading-tight uppercase">Welcome<br><span
                        class="text-blue-200">Bossing</span></h2>
                <p class="text-blue-100 font-bold tracking-wide">Authenticate to continue your <br> session in the
                    engine.</p>
            </div>
            <div class="text-[10px] font-black uppercase tracking-widest opacity-60">WHITE & BLUE // AUTH_SERVICE_V5
            </div>
        </div>
        <div class="flex items-center justify-center p-6 min-h-screen bg-gray-50">
            <form @submit.prevent="handleLogin"
                class="w-full max-w-md bg-white p-8 rounded-2xl border border-gray-200 shadow-sm space-y-6">

                <div class="space-y-1">
                    <router-link to="/" class="text-sm text-blue-600 hover:text-blue-800 flex items-center gap-1 mb-4">
                        &larr; Back to Home
                    </router-link>
                    <h1 class="text-2xl font-bold text-blue-900">Login</h1>
                    <p class="text-sm text-gray-500">Enter your credentials to access your account.</p>
                </div>

                <div v-if="errorMessage" class="p-4 text-sm text-red-700 bg-red-50 border border-red-200 rounded-lg">
                    {{ errorMessage }}
                </div>

                <div class="space-y-4">
                    <div class="flex flex-col gap-1.5">
                        <label class="text-sm font-medium text-gray-700">Email Address</label>
                        <input v-model="email"
                            class="w-full p-3 rounded-xl border border-gray-300 focus:ring-2 focus:ring-blue-500 outline-none transition"
                            type="email" placeholder="name@example.com" required>
                    </div>

                    <div class="flex flex-col gap-1.5">
                        <label class="text-sm font-medium text-gray-700">Password</label>
                        <div class="flex justify-between items-center relative">
                            <input v-model="password" :type="showPassword ? 'text' : 'password'"
                                class=" w-full p-3 rounded-xl border border-gray-300 focus:ring-2 focus:ring-blue-500 outline-none transition"
                                placeholder="••••••••" required>
                            <button type="button" @click="togglePassword"
                                class="absolute right-5 text-xs text-blue-600 hover:underline">
                                {{ showPassword ? 'Hide' : 'Show' }}
                            </button>
                        </div>

                    </div>
                </div>

                <div class="flex items-center justify-between">
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="checkbox"
                            class="w-4 h-4 rounded-lg border-gray-300 text-blue-600 focus:ring-blue-500">
                        <span class="text-sm text-gray-600">Remember me</span>
                    </label>
                    <span class="text-sm text-blue-600 cursor-pointer hover:underline">Forgot password?</span>
                </div>

                <button :disabled="isLoading" type="submit"
                    class="w-full py-3 rounded-xl bg-blue-600 text-white font-semibold hover:bg-blue-700 transition disabled:bg-blue-400">
                    {{ isLoading ? 'Authenticating...' : 'Sign In' }}
                </button>

                <p class="text-center text-sm text-gray-600">
                    Don't have an account?
                    <router-link to="/register" class="text-blue-600 font-semibold hover:underline">Sign
                        up</router-link>
                </p>
            </form>
        </div>
    </section>
</template>