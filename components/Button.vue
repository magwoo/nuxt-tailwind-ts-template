<script setup lang="ts">
    type ButtonType = "Regular" | "Primary";

    interface Props {
        type?: ButtonType
    }

    const { type = "Regular" } = defineProps<Props>();
    const emit = defineEmits(["click"]);

    const backgroundStyles = {
        "Regular": "bg-stone-300 rounded-xl text-stone-900",
        "Primary": "bg-blue-600 rounded-xl text-white"
    }[type];

    const foregroundStyles = {
        "Regular": "px-4 py-2 rounded-xl bg-stone-200",
        "Primary": "px-4 py-2 rounded-xl bg-blue-500"
    }[type];
</script>

<template>
    <button :class='backgroundStyles' @click='emit("click")'>
        <div :class='foregroundStyles' class='-translate-y-1 hover:-translate-y-1.5 active:-translate-y-0.5 transition-transform duration-75'>
            <slot />
        </div>
    </button>
</template>