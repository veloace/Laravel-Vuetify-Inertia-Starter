<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';

import {Head, useForm} from '@inertiajs/vue3';

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
    terms_and_conditions: false,
});
defineOptions({ layout: GuestLayout })

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
const appName = import.meta.env.VITE_APP_NAME || 'Laravel';

</script>

<template>
        <Head title="Register"/>

            <v-card class="mx-auto pa-4 pb-8" max-width="600" :loading="form.processing"
                    variant="elevated">
                <template v-slot:title  style="word-break: break-word;">
                    <h1 class="text-center">Sign Up!</h1>
                </template>
                <v-card-text>
                    <v-form>
                        <v-text-field class="mb-4" :error-messages="form.errors.name" placeholder="Enter your name"
                                      variant="outlined" id="name" type="text" v-model="form.name" required autofocus
                                      autocomplete="Full Name" label="Full Name"></v-text-field>
                        <v-text-field class="mb-4" :error-messages="form.errors.email" placeholder="Enter your email"
                                      variant="outlined" id="email" type="email" v-model="form.email" required autofocus
                                      autocomplete="username" label="Email Address"></v-text-field>
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
                                      label="Confirm Your Password"
                                      type="password"
                                      placeholder="confirm password"
                                      prepend-inner-icon="mdi-lock-outline"
                                      variant="outlined"
                                      v-model="form.password_confirmation"
                        ></v-text-field>

                        <v-checkbox class="mb-4"
                                    label="I am at least 13 years of age and I accept the terms and conditions."
                                    name="terms_and_conditions" v-model="form.terms_and_conditions"
                                    :error-messages="form.errors.terms_and_conditions"></v-checkbox>

                        <v-btn size="large" block @click="submit" color="green" :disabled="form.processing"
                               class="mt-4">Create Your Account
                        </v-btn>
                    </v-form>
                </v-card-text>
            </v-card>
</template>
