<script setup>
import { ref } from "vue";
import { Head, Link, router } from "@inertiajs/vue3";
import ApplicationMark from "@/Components/ApplicationMark.vue";
import Banner from "@/Components/Banner.vue";
import Dropdown from "@/Components/Dropdown.vue";
import ResponsiveNav from "@/Components/ResponsiveNav.vue";
import { Button } from "@/Components/ui/button";
import MainNav from "@/Components/ui/components/MainNav.vue";
import TeamSwitcher from "@/Components/TeamSwitcher.vue";
import UserNav from "@/Components/ui/components/UserNav.vue";
import Search from "@/Components/ui/components/Search.vue";

defineProps({
    title: String,
});
</script>

<template>
    <div class="app">
        <div class="hidden flex-col md:flex border-b">
            <div class="flex h-16 items-center container relative">
                <!-- Logo -->
                <div class="shrink-0 flex items-center">
                    <Link :href="route('dashboard')">
                        <ApplicationMark class="block h-8 w-auto" />
                    </Link>
                </div>
                <MainNav class="mx-6" />
                <div class="ml-auto flex items-center space-x-4">
                    <TeamSwitcher />
                    <Search />
                    <UserNav />
                </div>
            </div>
        </div>
        <ResponsiveNav />
        <main class="container relative pt-6">
            <slot />
        </main>
    </div>
</template>
