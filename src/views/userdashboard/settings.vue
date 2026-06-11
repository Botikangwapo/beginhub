<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from '../../supabase/supabase.js'
import { useRouter } from 'vue-router'
import { getAuthUser } from '../../services/authuserservices.js'

// ... (existing refs mo dito)
const fname = ref('Loading...')
const lname = ref('')
const email = ref('')
const avatarUrl = ref('')

const currentPassword = ref('');
const newPassword = ref('');
const confirmPassword = ref('');
const isLoading = ref(false);

// [DITO ANG IDADAGDAG NA FUNCTION]
const handleUpdatePassword = async () => {
    if (newPassword.value !== confirmPassword.value) {
        alert("New passwords do not match!");
        return;
    }

    if (newPassword.value.length < 8) {
        alert("Password must be at least 8 characters long.");
        return;
    }

    isLoading.value = true;

    try {
        // Supabase update password logic
        const { data, error } = await supabase.auth.updateUser({
            password: newPassword.value
        })

        if (error) throw error;

        alert("Password updated successfully!");

        // I-clear ang mga input pagkatapos ng success
        currentPassword.value = '';
        newPassword.value = '';
        confirmPassword.value = '';
    } catch (err) {
        console.error("Error updating password:", err.message);
        alert("Failed to update password: " + err.message);
    } finally {
        isLoading.value = false;
    }
}

onMounted(async () => {
    // ... (existing onMounted logic mo)
    const user = await getAuthUser();
    if (!user) return;

    if (user) {
        email.value = user.email

        const { data: profile, error: profileError } = await supabase
            .from('profiles')
            .select('first_name, last_name, avatar_url')
            .eq('id', user.id)
            .single()

        if (profile && !profileError) {
            fname.value = profile.first_name
            lname.value = profile.last_name
            avatarUrl.value = profile.avatar_url || `https://ui-avatars.com/api/?name=${profile.first_name}+${profile.last_name}&background=2563eb&color=fff&bold=true`
        } else {
            fname.value = 'Bossing'
            avatarUrl.value = `https://ui-avatars.com/api/?name=Bossing&background=2563eb&color=fff&bold=true`
        }
    }
})
</script>



<template>
    <section class="h-screen flex items-start justify-start p-6 flex-col">
        <div class="2xl:pt-0 w-full pt-14 border-b border-blue-50 pb-5">
            <div class="flex items-center gap-2">
                <h1 class="text-2xl font-black text-blue-900 tracking-tight uppercase">Settings</h1>
            </div>
            <p class="text-xs text-gray-700/70 mt-1">Manage your enterprise platform profile information and display
                preferences.</p>
        </div>
        <div class="2xl:w-200 w-full p-6  bg-white text-gray-900 rounded-lg">

            <section class="mb-8">
                <h2 class="text-lg font-black mb-4 text-blue-950">Profile information</h2>
                <div class="flex items-center gap-6 mb-6">
                    <img :src="avatarUrl"
                        class="w-16 h-16 bg-blue-100 text-blue-700 flex items-center justify-center rounded-lg font-bold text-xl" />


                    <div>
                        <button
                            class="px-4 py-2 border border-gray-200 rounded-xl text-sm hover:bg-gray-100 transition">
                            Change photo
                        </button>
                        <p class="text-xs text-gray-500 mt-2">JPG or PNG, max 800KB</p>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div>
                        <label class="block text-sm mb-2">Full name</label>
                        <div type="text" value="Juan Dela Cruz"
                            class="w-full bg-gray-50 border border-gray-200 rounded-xl p-2.5 focus:border-blue-500 outline-none">
                            {{ fname }} {{ lname }}
                        </div>
                    </div>
                    <div>
                        <label class="block text-sm mb-2">Email address</label>
                        <div type="email" value="juan@example.com"
                            class="w-full bg-gray-50 border border-gray-200 rounded-xl p-2.5 focus:border-blue-500 outline-none">
                            {{ email }}
                        </div>
                    </div>
                </div>
            </section>

            <section class="border-t border-gray-200 pt-6">
                <h2 class="text-lg font-black mb-4 text-blue-950">Update password</h2>

                <form @submit.prevent="handleUpdatePassword" class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium mb-2 text-gray-700">Current password</label>
                        <input v-model="currentPassword" type="password" placeholder="Enter current password"
                            class="w-full bg-gray-50 border border-gray-200 rounded-xl p-2.5 focus:border-blue-500 focus:ring-1 focus:ring-blue-500 outline-none transition"
                            required />
                    </div>

                    <div>
                        <label class="block text-sm font-medium mb-2 text-gray-700">New password</label>
                        <input v-model="newPassword" type="password" placeholder="At least 8 characters"
                            class="w-full bg-gray-50 border border-gray-200 rounded-xl p-2.5 focus:border-blue-500 focus:ring-1 focus:ring-blue-500 outline-none transition"
                            required />
                    </div>

                    <div>
                        <label class="block text-sm font-medium mb-2 text-gray-700">Confirm new password</label>
                        <input v-model="confirmPassword" type="password" placeholder="Repeat new password"
                            class="w-full bg-gray-50 border border-gray-200 rounded-xl p-2.5 focus:border-blue-500 focus:ring-1 focus:ring-blue-500 outline-none transition"
                            required />
                    </div>

                    <div class="mt-6 flex gap-3 justify-end">
                        <button type="button"
                            class="w-40 border border-gray-200 p-2.5 rounded-xl hover:bg-gray-50 transition font-medium">
                            Cancel
                        </button>
                        <button type="submit" :disabled="isLoading"
                            class="w-40 p-2.5 rounded-xl text-white bg-blue-600 hover:bg-blue-700 transition font-medium disabled:opacity-50">
                            {{ isLoading ? 'Saving...' : 'Save' }}
                        </button>
                    </div>
                </form>
            </section>
        </div>
    </section>
</template>
