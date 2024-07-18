<script setup>
import {Link, usePage, router} from '@inertiajs/vue3';
import NavLink from "@/Components/NavLink.vue";

const drawer = defineModel('drawer', {type: Boolean, default: false})
const pageLoading = defineModel('pageLoading', {type: Boolean, default: false})

const appName = import.meta.env.VITE_APP_NAME || 'Laravel';
const user = usePage().props.auth.user;

const navigateTo = (routeName) => {
    router.visit(route(routeName));
}

router.on('start', () => {
    pageLoading.value = true
})
router.on('finish', () => {
    pageLoading.value = false;
    drawer.value = false;
})

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
            <v-toolbar-title>{{ appName }}</v-toolbar-title>
            <template v-slot:append>

                <v-btn icon="mdi-account">
                    <v-icon></v-icon>
                    <v-menu activator="parent">
                        <v-list>
                            <v-list-item link @click="navigateTo('profile.edit')" title="My Account"></v-list-item>
                            <v-list-item link>
                                <Link :href="route('logout')" method="post" as="span">
                                    Logout
                                </Link>
                            </v-list-item>
                        </v-list>
                    </v-menu>
                </v-btn>

            </template>

        </v-app-bar>

        <v-navigation-drawer v-model="drawer" temporary>
            <v-sheet
                class="pa-4"
                color="grey-lighten-4"
            >
                <v-avatar
                    class="mb-4"
                    color="grey-darken-1"
                    size="64"
                ></v-avatar>

                <div>{{ user.name }}</div>

            </v-sheet>

            <v-divider></v-divider>

            <v-list>
                <nav-link routeName="dashboard">Dashboard</nav-link>
            </v-list>

        </v-navigation-drawer>

        <v-main>
            <v-container fluid class="d-flex justify-center">
                <slot/>
            </v-container>
            <v-footer class="d-flex flex-column px-0 py-0" app>
                <div class="bg-deep-purple-accent-1 d-flex w-100 align-center px-4">
                    <strong>Get connected with us on social networks!</strong>

                    <v-spacer></v-spacer>
                </div>

                <div class="px-4 py-2 bg-black text-center w-100">
                    &copy; {{ new Date().getFullYear() }} — <strong>{{ appName }}</strong>
                </div>
            </v-footer>
        </v-main>

    </v-layout>
</template>
