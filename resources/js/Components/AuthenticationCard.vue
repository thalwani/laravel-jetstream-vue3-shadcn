<script setup>
defineProps({
    title: String,
    description: String,
});
</script>

<template>
    <div
        class="w-full lg:grid h-lvh lg:min-h-[600px]"
    >
        <div class="flex items-center justify-center py-12">
            <div class="mx-auto grid gap-6">
                <div class="grid gap-2 text-center">
                    <h1 class="text-3xl font-bold">{{ title }}</h1>
                    <p class="text-balance text-muted-foreground">{{ description }}</p>
                </div>
                <slot />
            </div>
        </div>
    </div>
</template>
