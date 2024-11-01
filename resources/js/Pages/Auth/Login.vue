<script setup>
import { Head, Link, useForm } from "@inertiajs/vue3";
import AuthenticationCard from "@/Components/AuthenticationCard.vue";
import AuthenticationCardLogo from "@/Components/AuthenticationCardLogo.vue";
import Checkbox from "@/Components/Checkbox.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { Button } from "@/Components/ui/button";
import { Input } from "@/Components/ui/input";
import { Label } from "@/Components/ui/label";
import { Separator } from "@/Components/ui/separator";

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const form = useForm({
    email: "",
    password: "",
    remember: false,
});

const submit = () => {
    form.transform((data) => ({
        ...data,
        remember: form.remember ? "on" : "",
    })).post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};
</script>

<template>
    <Head title="Log in" />

    <AuthenticationCard title="Login" description="Enter your email below to login to your account">
        <div
            v-if="status"
            class="mb-4 font-medium text-sm text-green-600 dark:text-green-400"
        >
            {{ status }}
        </div>
        <form @submit.prevent="submit" class="grid gap-4">
            <div class="grid gap-2">
                <Label for="email">Email</Label>
                <Input
                    id="email"
                    type="email"
                    v-model="form.email"
                    placeholder="m@example.com"
                    required
                    autofocus
                    autocomplete="username"
                />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>
            <div class="grid gap-2">
                <div class="flex items-center">
                    <Label for="password">Password</Label>
                    <Link
                        v-if="canResetPassword"
                        :href="route('password.request')"
                        class="ml-auto inline-block text-sm underline"
                    >
                        Forgot your password?
                    </Link>
                </div>
                <Input
                    id="password"
                    type="password"
                    required
                    v-model="form.password"
                    autocomplete="current-password"
                />
                <InputError class="mt-2" :message="form.errors.password" />

                <div class="block mt-4">
                    <label class="flex items-center">
                        <Checkbox
                            v-model:checked="form.remember"
                            name="remember"
                        />
                        <span
                            class="ms-2 text-sm text-gray-600 dark:text-gray-400"
                            >Remember me</span
                        >
                    </label>
                </div>
            </div>
            <Button
                type="submit"
                class="w-full"
                :class="{ 'opacity-25': form.processing }"
                :disabled="form.processing"
            >
                Login
            </Button>
        </form>
        <Separator class="my-4" label="Ou" />
        <Button variant="outline" class="w-full"> Login with Google </Button>
        <div class="mt-4 text-center text-sm">
            Don't have an account?
            <Link :href="route('register')" class="underline"> Sign up </Link>
        </div>
    </AuthenticationCard>
</template>
