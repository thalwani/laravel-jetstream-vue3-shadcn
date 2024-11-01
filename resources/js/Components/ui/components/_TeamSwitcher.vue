<script setup lang="ts">
import { computed } from "vue";
import { Link, usePage, router } from "@inertiajs/vue3";
import { Avatar, AvatarFallback, AvatarImage } from "@/Components/ui/avatar";
import { Button } from "@/Components/ui/button";
import {
    Command,
    CommandEmpty,
    CommandGroup,
    CommandInput,
    CommandItem,
    CommandList,
    CommandSeparator,
} from "@/Components/ui/command";
import {
    Dialog,
    DialogContent,
    DialogDescription,
    DialogFooter,
    DialogHeader,
    DialogTitle,
    DialogTrigger,
} from "@/Components/ui/dialog";

import { Input } from "@/Components/ui/input";
import { Label } from "@/Components/ui/label";
import {
    Popover,
    PopoverContent,
    PopoverTrigger,
} from "@/Components/ui/popover";

import {
    Select,
    SelectContent,
    SelectItem,
    SelectTrigger,
    SelectValue,
} from "@/Components/ui/select";
import { cn } from "@/lib/utils";
import { ChevronDown, CheckIcon, CirclePlus } from "lucide-vue-next";
import { ref } from "vue";

const page = usePage();

const teams = computed(() => {
    return page.props.auth.user.all_teams.map((team) => {
        return {
            label: team.name,
            value: team.id,
        };
    });
});

const groups = [
    {
        teams: teams.value,
    },
];

type Team = (typeof groups)[number]["teams"][number];

const open = ref(false);
const showNewTeamDialog = ref(false);
const selectedTeam = ref<Team>(groups[0].teams[0]);

const switchToTeam = (team) => {
    router.put(
        route("current-team.update"),
        {
            team_id: parseInt(team.value),
        },
        {
            preserveState: false,
        }
    );
};
</script>

<template>
    <Dialog v-model:open="showNewTeamDialog">
        <Popover v-model:open="open">
            <PopoverTrigger as-child>
                <Button
                    variant="outline"
                    role="combobox"
                    aria-expanded="open"
                    aria-label="Select a team"
                    :class="cn('w-[200px] justify-between', $attrs.class ?? '')"
                >
                    {{ selectedTeam.label }}
                    <ChevronDown class="ml-auto h-4 w-4 shrink-0 opacity-50" />
                </Button>
            </PopoverTrigger>
            <PopoverContent class="w-[200px] p-0">
                <Command
                    :filter-function="
                        (list, term) =>
                            list.filter((i) =>
                                i.label?.toLowerCase()?.includes(term)
                            )
                    "
                >
                    <CommandList>
                        <CommandInput placeholder="Search team..." />
                        <CommandEmpty>No team found.</CommandEmpty>
                        <CommandGroup
                            v-for="group in groups"
                            :key="group.label"
                            :heading="group.label"
                        >
                            <CommandItem
                                v-for="team in group.teams"
                                :key="team.value"
                                :value="team"
                                class="text-sm"
                                @click="
                                                        switchToTeam(team)
                                                    "
                            >
                                    {{ team.label }}
                                <CheckIcon
                                    :class="
                                        cn(
                                            'ml-auto h-4 w-4',
                                            selectedTeam.value === team.value
                                                ? 'opacity-100'
                                                : 'opacity-0'
                                        )
                                    "
                                />
                            </CommandItem>
                        </CommandGroup>
                    </CommandList>
                    <CommandSeparator />
                    <CommandList>
                        <CommandGroup>
                            <CommandItem value="create-team">
                                <CirclePlus class="mr-2 h-5 w-5" />
                                <Link
                                    v-if="$page.props.jetstream.canCreateTeams"
                                    :href="route('teams.create')"
                                    :active="route().current('teams.create')"
                                >
                                    Create New Team
                                </Link>
                            </CommandItem>
                        </CommandGroup>
                    </CommandList>
                </Command>
            </PopoverContent>
        </Popover>
        <DialogContent>
            <DialogHeader>
                <DialogTitle>Create team</DialogTitle>
                <DialogDescription>
                    Add a new team to manage products and customers.
                </DialogDescription>
            </DialogHeader>
            <div>
                <div class="space-y-4 py-2 pb-4">
                    <div class="space-y-2">
                        <Label for="name">Team name</Label>
                        <Input id="name" placeholder="Acme Inc." />
                    </div>
                    <div class="space-y-2">
                        <Label for="plan">Subscription plan</Label>
                        <Select>
                            <SelectTrigger>
                                <SelectValue placeholder="Select a plan" />
                            </SelectTrigger>
                            <SelectContent>
                                <SelectItem value="free">
                                    <span class="font-medium">Free</span> -
                                    <span class="text-muted-foreground">
                                        Trial for two weeks
                                    </span>
                                </SelectItem>
                                <SelectItem value="pro">
                                    <span class="font-medium">Pro</span> -
                                    <span class="text-muted-foreground">
                                        $9/month per user
                                    </span>
                                </SelectItem>
                            </SelectContent>
                        </Select>
                    </div>
                </div>
            </div>
            <DialogFooter>
                <Button variant="outline" @click="showNewTeamDialog = false">
                    Cancel
                </Button>
                <Button type="submit"> Continue </Button>
            </DialogFooter>
        </DialogContent>
    </Dialog>
</template>
