<script setup>

import { useForm } from '@inertiajs/vue3';
import { nextTick, ref } from 'vue';

const confirmingUserDeletion = ref(false);
const passwordInput = ref(null);

const form = useForm({
    password: '',
});

const confirmUserDeletion = () => {
    confirmingUserDeletion.value = true;

    nextTick(() => passwordInput.value.focus());
};

const deleteUser = () => {
    form.delete(route('profile.destroy'), {
        preserveScroll: true,
        onSuccess: () => closeModal(),
        onError: () => passwordInput.value.focus(),
        onFinish: () => form.reset(),
    });
};

const closeModal = () => {
    confirmingUserDeletion.value = false;

    form.reset();
};
</script>

<template>
    <section>
        <header class="mb-4">
            <h2 class="text-red">Delete Account</h2>

            <p>
                Once your account is deleted, all of its resources and data will be permanently deleted. Before deleting
                your account, please download any data or information that you wish to retain. <strong class="text-red">This action cannot be undone!</strong>
            </p>
        </header>

        <v-btn color="red" @click="confirmUserDeletion">Delete Account</v-btn>

        <v-bottom-sheet v-model="confirmingUserDeletion">
            <v-card
                class="text-center"
                height="200"
            >
                <v-card-text>
                    <v-btn
                        variant="text"
                        @click="confirmingUserDeletion = !confirmingUserDeletion"
                    >
                        cancel
                    </v-btn>

                    <br>
                    <br>

                    <div>
                        <h2 class="text-red">
                            Are you sure you want to delete your account?
                        </h2>

                        <p class="mt-1 text-sm text-gray-600">
                            Once your account is deleted, all of its resources and data will be permanently deleted. Please
                            enter your password to confirm you would like to permanently delete your account.
                        </p>

                        <v-text-field class="mb-4"
                                      :error-messages="form.errors.password"
                                      label="password"
                                      type="password"
                                      placeholder="Enter your password"
                                      prepend-inner-icon="mdi-lock-outline"
                                      variant="outlined"
                                      v-model="form.password"
                                      @keyup.enter="deleteUser"
                        ></v-text-field>
                        <v-btn :disabled="form.processing" @click="deleteUser" color="red">Delete Account</v-btn>
                    </div>
                </v-card-text>
            </v-card>
        </v-bottom-sheet>
    </section>
</template>
