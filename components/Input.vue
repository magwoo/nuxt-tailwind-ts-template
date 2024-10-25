<script setup lang="ts">
    interface Props {
        placeholder?: string;
        type?: string;
    }

    const { placeholder = "", type = "text" } = defineProps<Props>();

    const valueModel = defineModel<number>();
</script>

<template>
    <div class='bg-stone-300 rounded-xl text-stone-900'>
        <input
            class='px-4 py-2 -translate-y-1 rounded-xl bg-stone-200 outline-none placeholder:text-stone-400' 
            :type='type'
            :placeholder='placeholder'
            v-model='valueModel'
        />
    </div>
</template>