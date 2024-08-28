<script setup>
import { reactive, onMounted, ref } from 'vue';
import { router } from '@inertiajs/vue3';
import AppLayout from '@/Layouts/AppLayout.vue';
import Form from './_partials/Form.vue';

const props = defineProps({
    user: Object,
    errors: Object,
    message: {
        type: String,
        default: null
    }
});

const message = ref(null);

const form = reactive({
    name: props.user.name,
    email: props.user.email,
    password: null,
    password_confirmation: null,
});

function submit() {
    router.put(`/user/${props.user.id}`, form, {
        onSuccess: (res) => {
            if (res.props.flash.message) {
                message.value = res.props.flash.message;

                setTimeout(() => {
                    message.value = null;
                }, 3000);
            }
        }
    });
}

onMounted(() => {
    console.log('mounted')
});

</script>

<template>
    <AppLayout title="Edit User">
        <template #header>
            Edit User
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="flex justify-center p-4 overflow-hidden bg-white shadow-xl dark:bg-gray-800">
                    <div class="w-full sm:w-[500px] md:w-[600px]">
                        <div v-if="message" class="p-4 mb-2 text-white bg-green-500 rounded">{{ message }}</div>
                        <form @submit.prevent="submit">
                            <Form :form="form" :errors="errors">
                                <template #buttons>
                                    <div class="flex justify-end mt-2">
                                        <button type="submit"
                                            class="px-3 py-2 text-sm font-semibold text-white bg-indigo-600 rounded-md shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                                            Save
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