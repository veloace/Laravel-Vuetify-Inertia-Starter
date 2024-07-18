<script setup>

import {Link, useForm, usePage} from '@inertiajs/vue3';

defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const user = usePage().props.auth.user;

const form = useForm({
    name: user.name,
    email: user.email,
});
</script>

<template>
    <section class="mb-10">
        <header>
            <h2>Account Information</h2>

            <p>
                Update your account information and email address.
            </p>
        </header>

        <v-form @submit.prevent="form.patch(route('profile.update'))" class="mt-6">
            <v-text-field class="mb-4" :error-messages="form.errors.name" placeholder="Enter your name"
                          variant="outlined" id="name" type="text" v-model="form.name" required autofocus
                          autocomplete="Full Name" label="Full Name">
            </v-text-field>

            <v-text-field class="mb-4" :error-messages="form.errors.email" placeholder="Enter your email"
                          variant="outlined" id="email" type="email" v-model="form.email" required autofocus
                          autocomplete="username" label="Email Address">

            </v-text-field>


            <v-btn type="submit" color="green" :disabled="form.processing">Save Changes</v-btn>
            <v-alert v-if="form.recentlySuccessful" class="mb-4 mt-4" type="success">Account Information Saved</v-alert>

        </v-form>

        <div v-if="mustVerifyEmail && user.email_verified_at === null" class="my-5">
            <v-alert type="info">
                Your email address is unverified. Some functionality may be limited or disabled until you verify your
                email address by clicking the link we sent to your inbox.
                <v-btn v-if="status !== 'verification-link-sent'" :disabled="form.processing">
                    <Link :href="route('verification.send')" method="post" as="button" >
                        Click here to re-send the verification email.
                    </Link>

                </v-btn>
            </v-alert>

            <v-alert type="success" v-show="status === 'verification-link-sent'" class="mt-4" closable >
                A new verification link has been sent to your email address.
            </v-alert>
        </div>
    </section>
</template>
