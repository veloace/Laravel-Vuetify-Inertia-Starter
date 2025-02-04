<script setup>
import { computed } from 'vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const props = defineProps({
    status: {
        type: String,
    },
});
defineOptions({ layout: GuestLayout })

const form = useForm({});

const verificationLinkSent = computed(() => props.status === 'verification-link-sent');

</script>

<template>
    <Head title="Email Verification" />
        <p>
            Thanks for signing up! Before getting started, could you verify your email address by clicking on the link
            we just emailed to you? If you didn't receive the email, we will gladly send you another.
        </p>
        <v-btn v-if="!verificationLinkSent" color="info">
            <Link :href="route('verification.send')" method="post" as="button" :disabled="form.processing" >
                Click here to re-send the verification email.
            </Link>
        </v-btn>

        <v-alert type="success" v-show="verificationLinkSent" class="mt-4" closable >
            A new verification link has been sent to your email address.
        </v-alert>
</template>
