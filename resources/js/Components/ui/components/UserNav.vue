<script setup lang="ts">
import { Link, router } from "@inertiajs/vue3";
import { Avatar, AvatarFallback, AvatarImage } from "@/Components/ui/avatar";
import { Button } from "@/Components/ui/button";
import {
    DropdownMenu,
    DropdownMenuContent,
    DropdownMenuGroup,
    DropdownMenuItem,
    DropdownMenuLabel,
    DropdownMenuSeparator,
    DropdownMenuShortcut,
    DropdownMenuTrigger,
} from "@/Components/ui/dropdown-menu";

const logout = () => {
    router.post(route("logout"));
};

const initials = (username) => {
    const name = username.split(" ");
    return `${name[0].charAt(0)}${name[1] ? name[1].charAt(0) : ""}`;
};
</script>

<template>
    <DropdownMenu>
        <DropdownMenuTrigger as-child>
            <Button variant="ghost" class="relative h-8 w-8 rounded-full">
                <Avatar class="h-8 w-8">
                    <AvatarFallback>{{ initials($page.props.auth.user.name) }}</AvatarFallback>
                </Avatar>
            </Button>
        </DropdownMenuTrigger>
        <DropdownMenuContent class="w-56" align="end">
            <DropdownMenuLabel class="font-normal flex">
                <div class="flex flex-col space-y-1">
                    <p class="text-sm font-medium leading-none">
                        {{ $page.props.auth.user.name }}
                    </p>
                    <p class="text-xs leading-none text-muted-foreground">
                        {{ $page.props.auth.user.email }}
                    </p>
                </div>
            </DropdownMenuLabel>
            <DropdownMenuSeparator />
            <DropdownMenuGroup>
                <DropdownMenuItem>
                    <Link class="w-full" :href="route('profile.show')"
                        >Profile</Link
                    >
                </DropdownMenuItem>
            </DropdownMenuGroup>
            <DropdownMenuSeparator />
            <DropdownMenuItem>
                <!-- Authentication -->
                <form @submit.prevent="logout" class="w-full">
                    <button class="w-full flex">Log Out</button>
                </form>
            </DropdownMenuItem>
        </DropdownMenuContent>
    </DropdownMenu>
</template>
