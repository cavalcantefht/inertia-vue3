<script setup>

</script>

<template>
    <table class="border-collapse border border-slate-400 ...">
        <thead v-if="$slots.thead">
            <slot name="thead"/>
        </thead>
        <tbody v-if="$slots.tbody">
            <slot name="tbody"/>
        </tbody>
    </table>
</template>
