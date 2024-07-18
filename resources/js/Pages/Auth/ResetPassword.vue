<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';

const props = defineProps({
    email: {
        type: String,
        required: true,
    },
    token: {
        type: String,
        required: true,
    },
});
defineOptions({ layout: GuestLayout })

const form = useForm({
    token: props.token,
    email: props.email,
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('password.store'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
        <Head title="Reset Password" />


        <v-card class="mx-auto pa-4 pb-8" max-width="600" :loading="form.processing"
                variant="elevated">
            <template v-slot:title>
                <h1 class="text-center">Reset Password</h1>
            </template>
            <v-card-text>
                <v-form>
                    <v-text-field class="mb-4" :error-messages="form.errors.email" placeholder="Enter your email"
                                  variant="outlined" id="email" type="email" v-model="form.email" required autofocus
                                  autocomplete="username" label="Email Address" disabled></v-text-field>
                    <v-text-field class="mb-4"
                                  :error-messages="form.errors.password"
                                  label="password"
                                  type="password"
                                  placeholder="Enter your password"
                                  prepend-inner-icon="mdi-lock-outline"
                                  variant="outlined"
                                  v-model="form.password"
                    ></v-text-field

                    >
                    <v-text-field class="mb-4"
                                  :error-messages="form.errors.password_confirmation"
                                  label="Confirm You Password"
                                  type="password"
                                  placeholder="Confirm Your Password"
                                  prepend-inner-icon="mdi-lock-outline"
                                  variant="outlined"
                                  v-model="form.password_confirmation"
                    ></v-text-field>

                    <v-btn size="large" block @click="submit" color="green" :disabled="form.processing"
                           class="mt-4">Reset Password
                    </v-btn>
                </v-form>
            </v-card-text>
        </v-card>
</template>
