<script setup>
import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';

const passwordInput = ref(null);
const currentPasswordInput = ref(null);

const form = useForm({
    current_password: '',
    password: '',
    password_confirmation: '',
});

const updatePassword = () => {
    form.put(route('password.update'), {
        preserveScroll: true,
        onSuccess: () => form.reset(),
        onError: () => {
            if (form.errors.password) {
                form.reset('password', 'password_confirmation');
            }
            if (form.errors.current_password) {
                form.reset('current_password');
            }
        },
    });
};
</script>

<template>
    <section class="mb-10">
        <header>
            <h2>Update Password</h2>

            <p>Ensure your account is using a long, random password to stay secure and never reuse passwords!</p>
        </header>

        <form @submit.prevent="updatePassword" class="mt-6 space-y-6">
            <v-text-field class="mb-4"
                          :error-messages="form.errors.current_password"
                          label="current password"
                          type="password"
                          placeholder="Enter your current password"
                          prepend-inner-icon="mdi-lock-outline"
                          variant="outlined"
                          v-model="form.current_password"
            ></v-text-field>

            <v-text-field class="mb-4"
                          :error-messages="form.errors.password"
                          label="new password"
                          type="password"
                          placeholder="Enter your new password"
                          prepend-inner-icon="mdi-lock-outline"
                          variant="outlined"
                          v-model="form.password"
            ></v-text-field>

            <v-text-field class="mb-4"
                          :error-messages="form.errors.password_confirmation"
                          label="Confirm Your Password"
                          type="password"
                          placeholder="Confirm your new password"
                          prepend-inner-icon="mdi-lock-outline"
                          variant="outlined"
                          v-model="form.password_confirmation"
            ></v-text-field>

            <v-btn type="submit" color="green" :disabled="form.processing">Update Password</v-btn>
            <v-alert v-if="form.recentlySuccessful"  class="mb-4 mt-4" type="success">Password Updated!</v-alert>
        </form>
    </section>
</template>
