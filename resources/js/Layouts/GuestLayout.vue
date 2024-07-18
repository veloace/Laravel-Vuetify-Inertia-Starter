<script setup>
import {router} from '@inertiajs/vue3';
import NavLink from "@/Components/NavLink.vue";

const drawer = defineModel('drawer', { type: Boolean, default: false })
const pageLoading = defineModel('pageLoading', { type: Boolean, default: false })

const appName = import.meta.env.VITE_APP_NAME || 'Laravel';
const navigateTo = (routeName) => {
    router.visit(route(routeName));
}

router.on('start', () =>{pageLoading.value = true})
router.on('finish', () => {pageLoading.value = false;drawer.value=false;})

</script>
<template>
    <v-layout class="rounded rounded-md">
        <v-app-bar color="deep-purple">
            <v-progress-linear
                active
                v-if="pageLoading"
                indeterminate
                color="green"
                absolute
                bottom
            ></v-progress-linear>
            <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
            <v-app-bar-title>{{ appName }}</v-app-bar-title>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" temporary>
            <v-list>
                <v-list>
                    <nav-link routeName="home">Home</nav-link>
                    <nav-link routeName="login">Login</nav-link>
                    <nav-link routeName="register">Register</nav-link>
                </v-list>
            </v-list>
        </v-navigation-drawer>
        <v-main>
            <v-container fluid>
                <slot/>
            </v-container>
        </v-main>
    </v-layout>
</template>
