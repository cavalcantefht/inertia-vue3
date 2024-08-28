<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    data: Object
})

const modifyLinks = computed(() => {
    const clearLinks = [...props.data.links];
    clearLinks.shift();
    clearLinks.pop();

    return clearLinks;
})
</script>

<template>
    <div class="flex justify-center w-full">
        <div class="flex items-center justify-between px-4 py-3 bg-white border-t border-gray-200 sm:px-6">
            <div class="flex justify-between flex-1 sm:hidden">
                <Link v-if="data.prev_page_url" :href="data.prev_page_url"
                    class="relative inline-flex items-center px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50">
                Previous</Link>
                <Link v-if="data.next_page_url" :href="data.next_page_url"
                    class="relative inline-flex items-center px-4 py-2 ml-3 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50">
                Next</Link>
            </div>
            <div class="hidden sm:flex sm:flex-1 sm:items-center sm:justify-between">
                <div>
                    <nav class="inline-flex -space-x-px rounded-md shadow-sm isolate" aria-label="Pagination">
                        <Link v-if="data.prev_page_url" :href="data.prev_page_url"
                            class="relative inline-flex items-center px-2 py-2 text-gray-400 rounded-l-md ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">
                        <<span class="sr-only">Previous</span>
                            </Link>
                            <!-- class="link.active ? z-10 bg-indigo-600 text-white focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600" -->
                            <Link v-for="link in modifyLinks" :key="link.label" :href="link.url"
                                :class="{ 'z-10 bg-indigo-600 hover:bg-indigo-500 text-white focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 ': link.active }"
                                class="relative inline-flex items-center px-4 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">
                            {{ link.label }}
                            </Link>

                            <Link v-if="data.next_page_url" :href="data.next_page_url"
                                class="relative inline-flex items-center px-2 py-2 text-gray-400 rounded-r-md ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">
                            >
                            <span class="sr-only">Next</span>
                            </Link>
                    </nav>
                </div>
            </div>
        </div>
    </div>
</template>