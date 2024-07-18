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
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});

defineOptions({layout: GuestLayout})
const appName = import.meta.env.VITE_APP_NAME || 'Laravel';
const navigateTo = (routeName) => {
    router.visit(route(routeName));
}

function handleImageError() {
    document.getElementById('screenshot-container')?.classList.add('!hidden');
    document.getElementById('docs-card')?.classList.add('!row-span-1');
    document.getElementById('docs-card-content')?.classList.add('!flex-row');
    document.getElementById('background')?.classList.add('!hidden');
}

</script>
<script>
</script>

<template>
    <Head title="Welcome"/>
    <v-main class="d-flex align-center justify-center">
        <div>
            <h1 class="text-center">Welcome to {{ appName }}</h1>
            <p class="text-center">Please Login or Sign-up to get started!</p>
            <p class="text-center">
                <v-btn :href="route('login')" @click.prevent.stop="navigateTo('login')" class="mx-2" color="green">
                    Login
                </v-btn>
                <v-btn :href="route('register')" @click.prevent.stop="navigateTo('register')" class="mx-2" color="blue">
                    Create Account
                </v-btn>
            </p>

        </div>
    </v-main>
</template>
