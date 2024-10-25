<script setup lang="ts">
    interface Props {
        options: string[];
    }

    const props = defineProps<Props>();

    const emit = defineEmits(["change"]);

    const select = useTemplateRef("select");
</script>

<template>
    <div class='bg-stone-300 rounded-xl'>
        <select
            class='bg-stone-200 text-center cursor-pointer rounded-xl px-4 py-2 outline-none appearance-none -translate-y-1 hover:-translate-y-1.5 transition-transform duration-75'
            ref='select'
            @change="$emit('change', select?.value)"
        >
            <option v-for='option in props.options' :value='option' :disabled='option.startsWith(" ")'>{{ option }}</option>
        </select>
    </div>
</template>