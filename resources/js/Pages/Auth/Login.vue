<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, Link, useForm, router  } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});
defineOptions({ layout: GuestLayout })

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
const appName = import.meta.env.VITE_APP_NAME || 'Laravel';
const  visible = false;

const navigateTo = (routeName) => {
    router.visit(route(routeName));
}
</script>

<template>
        <Head title="Log in" />
            <v-card class="mx-auto pa-4 pb-8  " max-width="600" :loading="form.processing" variant="elevated">
                <template v-slot:title>
                    <h1 class="text-center" >Login</h1>
                </template>
                <v-card-text>
                    <v-alert v-if="status!== null" closable :text="status" class="mb-4 mt-4" type="success"></v-alert>

                    <v-form @submit.prevent="submit">
                        <v-text-field class="mb-6" :error-messages="form.errors.email" placeholder="Enter your email" variant="outlined"  id="email" type="email" v-model="form.email" required autofocus autocomplete="username" label="email"></v-text-field>
                        <v-text-field
                            :error-messages="form.errors.password"
                            label="password"
                            :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
                            :type="visible ? 'text' : 'password'"
                            placeholder="Enter your password"
                            prepend-inner-icon="mdi-lock-outline"
                            variant="outlined"
                            @click:append-inner="visible = !visible"
                            v-model="form.password"
                        ></v-text-field>
                        <v-checkbox label="Remember Me" name="remember" v-model="form.remember"></v-checkbox>
                        <v-btn block size="large" type="submit" color="deep-purple" :disabled="form.processing">Login</v-btn>
                    </v-form>
                </v-card-text>
                <p class="mt-5 text-right">
                    <Link v-if="canResetPassword" :href="route('password.request')" class="">Forgot your password?</Link>
                </p>
                <hr class="mt-5 mb-5">
                <p class="text-center">
                    <v-btn  :href="route('register')" @click.prevent.stop="navigateTo('register')" color="green" >Create an Account</v-btn>

                </p>
            </v-card>
</template>
