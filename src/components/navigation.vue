<template>
    <transition name="slide-down">
        <div v-if="open"
            class="fixed top-[64px] left-0 w-full z-[999] bg-white shadow-lg p-3 rounded-b-lg pointer-events-auto">
            <div class="w-full sm:flex grid gap-2 items-center">
                <a href="#home" @click.prevent="handleNav('#home')"
                    class="p-3 text-sm text-gray-600 font-light hover:text-blue-500 transition-colors duration-200 ansition-all after:duration-300 ">Home
                </a>
                <a href="#category" @click.prevent="handleNav('#category')"
                    class="p-3 text-sm text-gray-600 font-light hover:text-blue-500 transition-colors duration-200 ansition-all after:duration-300">Category
                    Filter
                </a>
                <a href="#resources" @click.prevent="handleNav('#resources')"
                    class="p-3 text-sm text-gray-600 font-light hover:text-blue-500 transition-colors duration-200 ansition-all after:duration-300 ">ResourcesList
                </a>
                <a href="#choose" @click.prevent="handleNav('#choose')"
                    class="p-3 text-sm text-gray-600 font-light hover:text-blue-500 transition-colors duration-200 ansition-all after:duration-300 ">Start
                    Quiz
                </a>
                <div class="grid sm:w-auto w-full gap-3 sm:flex">
                    <router-link to="/Login" @click="emit('close')"
                        class="sm:px-4 sm:py-2 px-0 py-3 text-sm rounded-lg font-light bg-white text-gray-900 sm:w-auto w-full text-center items-center flex justify-center">Login
                    </router-link>
                    <router-link to="/register" @click="emit('close')"
                        class="text-white sm:px-4 sm:py-2 px-0 py-3 text-sm rounded-lg font-light bg-blue-600 hover:bg-blue-500 w-full items-center flex justify-center">Get
                        started
                    </router-link>
                </div>
            </div>
        </div>
    </transition>
</template>

<script setup>
const props = defineProps({ open: Boolean })
const emit = defineEmits(['close'])

const handleNav = (href) => {
    console.log("Navigating to:", href); // Check mo sa Console kung lumalabas ito

    if (href.startsWith('#')) {
        const target = document.querySelector(href);
        console.log("Target element found:", target); // Check kung null o may laman

        if (target) {
            target.scrollIntoView({ behavior: 'smooth' });
        }
    }

    setTimeout(() => {
        console.log("Closing menu...");
        emit('close');
    });
}
</script>

<style scoped>
.slide-down-enter-from,
.slide-down-leave-to {
    transform: translateY(-10px);
    opacity: 0;
}

.slide-down-enter-to,
.slide-down-leave-from {
    transform: translateY(0);
    opacity: 1;
}

.slide-down-enter-active,
.slide-down-leave-active {
    transition: transform 180ms ease-out, opacity 180ms ease-out;
}
</style>