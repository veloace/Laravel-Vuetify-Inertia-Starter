<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';

import {Head, useForm} from '@inertiajs/vue3';

defineProps({
    status: {
        type: String,
    },
});
defineOptions({ layout: GuestLayout })

const form = useForm({
    email: '',
});

const submit = () => {
    form.post(route('password.email'));
};
</script>


<template>
    <Head title="Forgot Password"/>
            <v-card class="mx-auto pa-4 pb-8 " max-width="600" :loading="form.processing"
                    variant="elevated">
                <template v-slot:title>
                    <h2 class="text-center">Forgot Password?</h2>
                </template>

                <v-card-text>
                    <p class="mb-8"> Forgot your password? No problem. Just let us know your email address and we will
                        email you a
                        password reset link that will allow you to choose a new one.</p>
                    <v-alert v-if="status!== null" closable :text="status" class="mb-4 mt-4" type="success"></v-alert>
                    <v-form>
                        <v-text-field class="mb-6" :error-messages="form.errors.email" placeholder="Enter your email"
                                      variant="outlined" id="email" type="email" v-model="form.email" required autofocus
                                      autocomplete="username" label="email"></v-text-field>
                    </v-form>
                    <v-btn size="large" block @click="submit" color="green" :disabled="form.processing" class="mt-4">
                        Email Reset Link
                    </v-btn>


                </v-card-text>
            </v-card>
</template>
