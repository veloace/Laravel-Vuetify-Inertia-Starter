<script setup>
import {router} from "@inertiajs/vue3";
defineProps({
    routeName: {
        type: String,
    }
});
const navigateTo = (routeName) => {
    router.visit(route(routeName));
}

</script>

<template>
    <v-list-item link @click.prevent.stop="navigateTo(routeName)"  :active="route().current()===routeName">
        <slot></slot>
    </v-list-item>
</template>
