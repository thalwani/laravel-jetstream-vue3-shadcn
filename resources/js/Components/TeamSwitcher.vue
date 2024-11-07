<script setup>
import { ref } from "vue";
import { Head, Link, router } from "@inertiajs/vue3";
import Dropdown from "@/Components/Dropdown.vue";
import DropdownLink from "@/Components/DropdownLink.vue";

defineProps({
    title: String,
});

const showingNavigationDropdown = ref(false);

const switchToTeam = (team) => {
    router.put(
        route("current-team.update"),
        {
            team_id: team.id,
        },
        {
            preserveState: false,
        }
    );
};

const logout = () => {
    router.post(route("logout"));
};
</script>

<template>
    <!-- Teams Dropdown -->
    <Dropdown
        v-if="$page.props.jetstream.hasTeamFeatures"
        align="right"
        width="60"
    >
        <template #trigger>
            <span class="inline-flex rounded-md">
                <button
                    type="button"
                    class="inline-flex items-center whitespace-nowrap rounded-md text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50 border border-input bg-background shadow-sm hover:bg-accent hover:text-accent-foreground h-10 px-4 py-2 w-[200px] justify-between"
                >
                    {{ $page.props.auth.user.current_team.name }}

                    <svg
                        class="ms-2 -me-0.5 h-4 w-4"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M8.25 15L12 18.75 15.75 15m-7.5-6L12 5.25 15.75 9"
                        />
                    </svg>
                </button>
            </span>
        </template>

        <template #content>
            <div class="w-60">
                <!-- Team Management -->
                <div class="block px-4 py-2 text-xs text-gray-400">
                    {{ $t("Manage Team") }}
                </div>

                <!-- Team Settings -->
                <DropdownLink
                    :href="
                        route('teams.show', $page.props.auth.user.current_team)
                    "
                >
                    {{ $t("Team Settings") }}
                </DropdownLink>

                <DropdownLink
                    v-if="$page.props.jetstream.canCreateTeams"
                    :href="route('teams.create')"
                >
                    {{ $t("Create New Team") }}
                </DropdownLink>

                <!-- Team Switcher -->
                <template v-if="$page.props.auth.user.all_teams.length > 1">
                    <div
                        class="border-t border-gray-200 dark:border-gray-600"
                    />

                    <div class="block px-4 py-2 text-xs text-gray-400">
                        {{ $t("Switch Team") }}
                    </div>

                    <template
                        v-for="team in $page.props.auth.user.all_teams"
                        :key="team.id"
                    >
                        <form @submit.prevent="switchToTeam(team)">
                            <DropdownLink as="button">
                                <div class="flex items-center">
                                    <svg
                                        v-if="
                                            team.id ==
                                            $page.props.auth.user
                                                .current_team_id
                                        "
                                        class="me-2 h-5 w-5 text-green-400"
                                        xmlns="http://www.w3.org/2000/svg"
                                        fill="none"
                                        viewBox="0 0 24 24"
                                        stroke-width="1.5"
                                        stroke="currentColor"
                                    >
                                        <path
                                            stroke-linecap="round"
                                            stroke-linejoin="round"
                                            d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                                        />
                                    </svg>

                                    <div>
                                        {{ team.name }}
                                    </div>
                                </div>
                            </DropdownLink>
                        </form>
                    </template>
                </template>
            </div>
        </template>
    </Dropdown>
</template>
