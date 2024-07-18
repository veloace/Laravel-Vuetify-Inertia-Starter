<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';
import {Head} from '@inertiajs/vue3';

defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});
defineOptions({ layout: AuthenticatedLayout })

</script>

<template>
    <Head title="Your Account"/>
        <v-sheet class="pa-12 " :elevation="2" max-width="800px" >
            <UpdateProfileInformationForm
                :must-verify-email="mustVerifyEmail"
                :status="status"
                class="max-w-xl"
            />
            <v-divider></v-divider>
            <UpdatePasswordForm/>
            <v-divider></v-divider>

            <DeleteUserForm/>
        </v-sheet>
</template>
