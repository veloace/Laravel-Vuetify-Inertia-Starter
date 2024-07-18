<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';

defineOptions({ layout: AuthenticatedLayout })

</script>

<template>
    <Head title="Dashboard" />
    <div>
        <header >
            <h2 class="">Dashboard</h2>
        </header>
        <div class="py-12">
            <p>You're logged in!</p>
        </div>
    </div>

</template>
