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

    <AuthenticationCard
        :title="$t('Log in')"
        :description="$t('Enter your email to log in')"
    >
        <div
            v-if="status"
            class="mb-4 font-medium text-sm text-green-600 dark:text-green-400"
        >
            {{ status }}
        </div>
        <div class="grid grid-cols-2 gap-6">
            <Button variant="outline">
                <svg
                    class="mr-2 h-6 w-6"
                    x="0px"
                    y="0px"
                    width="100"
                    height="100"
                    viewBox="0 0 30 30"
                >
                    <path
                        d="M15,3C8.373,3,3,8.373,3,15c0,6.016,4.432,10.984,10.206,11.852V18.18h-2.969v-3.154h2.969v-2.099c0-3.475,1.693-5,4.581-5 c1.383,0,2.115,0.103,2.461,0.149v2.753h-1.97c-1.226,0-1.654,1.163-1.654,2.473v1.724h3.593L19.73,18.18h-3.106v8.697 C22.481,26.083,27,21.075,27,15C27,8.373,21.627,3,15,3z"
                    ></path>
                </svg>
                Facebook
            </Button>
            <Button variant="outline">
                <svg role="img" viewBox="0 0 24 24" class="mr-2 h-4 w-4">
                    <path
                        fill="currentColor"
                        d="M12.48 10.92v3.28h7.84c-.24 1.84-.853 3.187-1.787 4.133-1.147 1.147-2.933 2.4-6.053 2.4-4.827 0-8.6-3.893-8.6-8.72s3.773-8.72 8.6-8.72c2.6 0 4.507 1.027 5.907 2.347l2.307-2.307C18.747 1.44 16.133 0 12.48 0 5.867 0 .307 5.387.307 12s5.56 12 12.173 12c3.573 0 6.267-1.173 8.373-3.36 2.16-2.16 2.84-5.213 2.84-7.667 0-.76-.053-1.467-.173-2.053H12.48z"
                    ></path>
                </svg>
                Google
            </Button>
        </div>
        <Separator :label="$t('Or continue with')" />
        <form @submit.prevent="submit" class="grid gap-4">
            <div class="grid gap-2">
                <Label for="email">{{ $t("Email") }}</Label>
                <Input
                    id="email"
                    type="email"
                    v-model="form.email"
                    required
                    autofocus
                    autocomplete="username"
                />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>
            <div class="grid gap-2">
                <div class="flex items-center">
                    <Label for="password">{{ $t("Password") }}</Label>
                    <Link
                        v-if="canResetPassword"
                        :href="route('password.request')"
                        class="ml-auto inline-block text-sm underline"
                    >
                        {{ $t("Forgot your password?") }}
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
                        >
                            {{ $t("Remember me") }}
                        </span>
                    </label>
                </div>
            </div>
            <Button
                type="submit"
                class="w-full"
                :class="{ 'opacity-25': form.processing }"
                :disabled="form.processing"
            >
                {{ $t("Log in") }}
            </Button>
        </form>
        <div class="text-center text-sm">
            {{ $t("Dont Have An Account?") }}
            <Link :href="route('register')" class="underline">{{
                $t("Register")
            }}</Link>
        </div>
    </AuthenticationCard>
</template>
