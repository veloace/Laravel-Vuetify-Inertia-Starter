<script setup>
import {Head, router} from '@inertiajs/vue3';
import GuestLayout from "@/Layouts/GuestLayout.vue";

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
});

defineOptions({layout: GuestLayout})
const appName = import.meta.env.VITE_APP_NAME || 'Laravel';
</script>
<template>
    <Head title="Welcome"/>
    <v-main class="d-flex align-center justify-center">
        <div>
            <h1 class="text-center">Welcome to {{ appName }}</h1>
            <p class="text-center">Please Login or Sign-up to get started!</p>
            <p class="text-center">
                <v-btn :href="route('login')" @click.prevent.stop="router.visit(route('login'))" class="mx-2" color="green">
                    Login
                </v-btn>
                <v-btn :href="route('register')" @click.prevent.stop=" router.visit(route('register'))" class="mx-2" color="blue">
                    Create Account
                </v-btn>
            </p>

        </div>
    </v-main>
</template>
