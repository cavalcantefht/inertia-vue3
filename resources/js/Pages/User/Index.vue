<script setup>
import { ref } from 'vue';
import { Link, router } from "@inertiajs/vue3";
import AppLayout from "@/Layouts/AppLayout.vue";
import Table from "@/Components/Table.vue";
import Paginate from "@/Components/Paginate.vue";
import ConfirmationModal from "@/Components/ConfirmationModal.vue";
import DangerButton from "@/Components/DangerButton.vue";
import SecondaryButton from "@/Components/SecondaryButton.vue";
import ActionMessage from "@/Components/ActionMessage.vue";

defineProps({
    users: Object
});

const modalDelete = ref(false);
const userDelete = ref(null);
const message = ref(null);

function deleteUser(user) {
    userDelete.value = user;
    modalDelete.value = true;
}

function confirmDeleteUser() {
    const user = userDelete.value;
    router.delete(`/user/${user.id}`, {
        onSuccess: (res) => {
            modalDelete.value = false;
            if (res.props.flash.message) {
                message.value = res.props.flash.message;

                setTimeout(() => {
                    message.value = null;
                }, 3000);
            }
        }
    });
}
</script>
<template>
    <AppLayout title="Users">
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800 dark:text-gray-200">
                Users
            </h2>
        </template>
        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-xl dark:bg-gray-800 sm:rounded-lg">

                    <div class="w-full p-4">
                        <div class="flex justify-end p-2">
                            <Link :href="route('user.create')"
                                class="px-3 py-2 text-sm font-semibold text-white bg-indigo-600 rounded-md shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                            New User
                            </Link>
                        </div>

                        <div v-if="message" class="w-full p-2 mb-2 text-white bg-green-500 rounded">
                            {{ message }}
                        </div>

                        <div>
                            <Table class="w-full">
                                <template #thead>
                                    <tr>
                                        <th class="text-center border border-slate-300">ID</th>
                                        <th class="text-center border border-slate-300">User Name</th>
                                        <th class="text-center border border-slate-300">Email</th>
                                        <th class="text-center border border-slate-300"></th>
                                    </tr>
                                </template>
                                <template #tbody v-if="users.data.length">
                                    <tr v-for="user in users.data" :key="user.id">
                                        <td class="text-center border border-slate-300">{{ user.id }}</td>
                                        <td class="text-center border border-slate-300">{{ user.name }}</td>
                                        <td class="text-center border border-slate-300">{{ user.email }}</td>
                                        <td class="text-center border border-slate-300">
                                            <Link :href="route('user.edit', { user })">Edit</Link>
                                            <button class="p-2 ml-2 text-red-500"
                                                @click="deleteUser(user)">Delete</button>
                                        </td>
                                    </tr>
                                </template>
                            </Table>
                        </div>
                        <Paginate :data="users" />

                        <ConfirmationModal :show="modalDelete" @close="modalDelete = false">
                            <template #title>
                                Exclusão de Usuário
                            </template>
                            <template #content>
                                Confirma a exclusão deste usuário?
                            </template>
                            <template #footer>
                                <SecondaryButton @click="modalDelete = false">
                                    Cancelar
                                </SecondaryButton>
                                &nbsp;
                                <DangerButton @click="confirmDeleteUser">
                                    Confirmar
                                </DangerButton>
                            </template>
                        </ConfirmationModal>

                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
