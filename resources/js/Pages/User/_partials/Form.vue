<script setup>

defineProps({
    form: Object,
    errors: Object
});

</script>

<template>
    <div>
        <div class="sm:col-span-3">
            <label for="name" class="block text-sm font-medium leading-6 text-gray-900">
                Name
            </label>
            <div class="mt-2">
                <input type="text" id="name" v-model="form.name"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                <div v-if="errors.name" class="p-2 mt-1 text-white bg-red-500 rounded">{{ errors.name }}</div>

            </div>
        </div>

        <div class="sm:col-span-3">
            <label for="email" class="block text-sm font-medium leading-6 text-gray-900">
                E-mail
            </label>
            <div class="mt-2">
                <input type="email" id="email" v-model="form.email"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                <div v-if="errors.email" class="p-2 mt-1 text-white bg-red-500 rounded">{{ errors.email }}</div>
            </div>
        </div>

        <div class="sm:col-span-3">
            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">
                Password
            </label>
            <div class="mt-2">
                <input type="password" id="password" v-model="form.password"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                <div v-if="errors.password" class="p-2 mt-1 text-white bg-red-500 rounded">{{ errors.password }}</div>
            </div>
        </div>

        <div class="sm:col-span-3">
            <label for="password-confirmation" class="block text-sm font-medium leading-6 text-gray-900">
                Password Confirmation
            </label>
            <div class="mt-2">
                <input type="password" id="password-confirmation" v-model="form.password_confirmation"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
            </div>
        </div>
        <slot v-if="$slots.buttons" name="buttons" />
    </div>
</template>