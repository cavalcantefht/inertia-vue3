<script setup>
import { reactive, ref } from 'vue';
import { router } from '@inertiajs/vue3';
import AppLayout from '@/Layouts/AppLayout.vue';
import Form from './_partials/Form.vue';

defineProps({ errors: Object })

const message = ref(null);

const form = reactive({
    name: null,
    email: null,
    password: null,
    password_confirmation: null,
});

function submit() {
    router.post('/user', form, {
        onSuccess: (res) => {
            message.value = res.props.flash.message;

            form.name = null;
            form.email = null;
            form.password = null;
            form.password_confirmation = null;

            setTimeout(() => {
                message.value = '';
            }, 3000)
        }
    });
}

</script>

<template>
    <AppLayout title="Create User">
        <template #header>
            Create User
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="p-4 overflow-hidden bg-white shadow-xl dark:bg-gray-800 sm:rounded-lg">
                    <div class="w-full sm:w-[500px] md:w-[600px]">
                        <div v-if="message" class="p-4 mb-2 text-white bg-green-500 rounded">{{ message }}</div>
                        <form @submit.prevent="submit">
                            <Form :form="form" :errors="errors">
                                <template #buttons>
                                    <div class="flex justify-end mt-2">
                                        <button type="reset"
                                            class="px-3 py-2 text-sm font-semibold text-white bg-indigo-600 rounded-md shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                                            Reset
                                        </button>
                                        &nbsp;
                                        <button type="submit"
                                            class="px-3 py-2 text-sm font-semibold text-white bg-indigo-600 rounded-md shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                                            Create
                                        </button>
                                    </div>
                                </template>
                            </Form>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>