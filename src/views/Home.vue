<script setup>
import { ref } from 'vue';
import Navbar from '../components/navbar.vue';
import Hero from '../components/hero.vue';
import Resources from '../components/resources.vue';
import Footer from '../components/footer.vue';
import Navigation from '../components/navigation.vue';

const showNav = ref(false); // Dito ang source of truth
</script>

<!-- Reusable Components -->
<template>
    <Navbar v-model:showNav="showNav" />
    <Navigation :open="showNav" @close="showNav = false" />
    <!-- Home -->
    <section :class="showNav ? '2xl:pt-0 pt-[240px]' : 'pt-0'" class="transition-all duration-300 ease-in-out">
        <Hero />
        <!-- <Category /> -->
        <Resources />
        <Footer />
    </section>

</template>

<style></style>