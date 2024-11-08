<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import { Badge } from "@/Components/ui/badge";
import { Button } from "@/Components/ui/button";
import { Input } from "@/Components/ui/input";
import DateRangePicker from "@/Components/ui/components/DateRangePicker.vue";
import Overview from "@/Components/ui/components/Overview.vue";
import RecentSales from "@/Components/ui/components/RecentSales.vue";

const tab = []

import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '@/Components/ui/card'
import {
  Tabs,
  TabsContent,
  TabsList,
  TabsTrigger,
} from '@/Components/ui/tabs'
  import { Avatar, AvatarFallback, AvatarImage } from "@/Components/ui/avatar";
</script>

<template>
    <AppLayout :title="$t('Dashboard')">
        <div class="flex-1 space-y-4">
            <div class="flex items-center justify-between space-y-2">
                <h2 class="text-3xl font-bold tracking-tight">{{ $t('Dashboard') }}</h2>
                <div class="flex items-center space-x-2">
                    <DateRangePicker />
                    <Button>{{ $t('Filter') }}</Button>
                </div>
            </div>
            <Tabs default-value="overview" class="space-y-4">
                <TabsList>
                    <TabsTrigger value="overview"> {{ $t('Overview') }} </TabsTrigger>
                    <TabsTrigger value="analytics" disabled>
                        {{ $t('Analytics') }}
                    </TabsTrigger>
                    <TabsTrigger value="reports" disabled>
                        {{ $t('Reports') }}
                    </TabsTrigger>
                    <TabsTrigger value="notifications" disabled>
                        {{ $t('Notifications') }}
                    </TabsTrigger>
                </TabsList>
                <TabsContent value="overview" class="space-y-4">
                    <div class="grid gap-4 md:grid-cols-2 lg:grid-cols-4">
                        <Card>
                            <CardHeader
                                class="flex flex-row items-center justify-between space-y-0 pb-2"
                            >
                                <CardTitle class="text-sm font-medium">
                                    {{ $t('Total Revenue') }}
                                </CardTitle>
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    viewBox="0 0 24 24"
                                    fill="none"
                                    stroke="currentColor"
                                    strokeLinecap="round"
                                    strokeLinejoin="round"
                                    strokeWidth="2"
                                    class="h-4 w-4 text-muted-foreground"
                                >
                                    <path
                                        d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"
                                    />
                                </svg>
                            </CardHeader>
                            <CardContent>
                                <div class="text-2xl font-bold">$45,231.89</div>
                                <p class="text-xs text-muted-foreground">
                                    +20.1% {{ $t('from last month') }}
                                </p>
                            </CardContent>
                        </Card>
                        <Card>
                            <CardHeader
                                class="flex flex-row items-center justify-between space-y-0 pb-2"
                            >
                                <CardTitle class="text-sm font-medium">
                                    {{ $t('Subscriptions') }}
                                </CardTitle>
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    viewBox="0 0 24 24"
                                    fill="none"
                                    stroke="currentColor"
                                    strokeLinecap="round"
                                    strokeLinejoin="round"
                                    strokeWidth="2"
                                    class="h-4 w-4 text-muted-foreground"
                                >
                                    <path
                                        d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"
                                    />
                                    <circle cx="9" cy="7" r="4" />
                                    <path
                                        d="M22 21v-2a4 4 0 0 0-3-3.87M16 3.13a4 4 0 0 1 0 7.75"
                                    />
                                </svg>
                            </CardHeader>
                            <CardContent>
                                <div class="text-2xl font-bold">+2350</div>
                                <p class="text-xs text-muted-foreground">
                                    +180.1% {{ $t('from last month') }}
                                </p>
                            </CardContent>
                        </Card>
                        <Card>
                            <CardHeader
                                class="flex flex-row items-center justify-between space-y-0 pb-2"
                            >
                                <CardTitle class="text-sm font-medium">
                                    {{ $t('Sales') }}
                                </CardTitle>
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    viewBox="0 0 24 24"
                                    fill="none"
                                    stroke="currentColor"
                                    strokeLinecap="round"
                                    strokeLinejoin="round"
                                    strokeWidth="2"
                                    class="h-4 w-4 text-muted-foreground"
                                >
                                    <rect
                                        width="20"
                                        height="14"
                                        x="2"
                                        y="5"
                                        rx="2"
                                    />
                                    <path d="M2 10h20" />
                                </svg>
                            </CardHeader>
                            <CardContent>
                                <div class="text-2xl font-bold">+12,234</div>
                                <p class="text-xs text-muted-foreground">
                                    +19% {{ $t('from last month') }}
                                </p>
                            </CardContent>
                        </Card>
                        <Card>
                            <CardHeader
                                class="flex flex-row items-center justify-between space-y-0 pb-2"
                            >
                                <CardTitle class="text-sm font-medium">
                                    {{ $t('Active Now') }}
                                </CardTitle>
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    viewBox="0 0 24 24"
                                    fill="none"
                                    stroke="currentColor"
                                    strokeLinecap="round"
                                    strokeLinejoin="round"
                                    strokeWidth="2"
                                    class="h-4 w-4 text-muted-foreground"
                                >
                                    <path d="M22 12h-4l-3 9L9 3l-3 9H2" />
                                </svg>
                            </CardHeader>
                            <CardContent>
                                <div class="text-2xl font-bold">+573</div>
                                <p class="text-xs text-muted-foreground">
                                    +201 {{ $t('since last hour') }}
                                </p>
                            </CardContent>
                        </Card>
                    </div>
                    <div class="grid gap-4 md:grid-cols-2 lg:grid-cols-7">
                        <Card class="col-span-4">
                            <CardHeader>
                                <CardTitle>{{ $t('Overview') }}</CardTitle>
                            </CardHeader>
                            <CardContent class="pl-2">
                                <Overview />
                            </CardContent>
                        </Card>
                        <Card class="col-span-3">
                            <CardHeader>
                                <CardTitle>{{ $t('Recent Sales') }}</CardTitle>
                                <CardDescription>
                                    {{ $t('Sales this month.') }}
                                </CardDescription>
                            </CardHeader>
                            <CardContent>
                                <RecentSales />
                            </CardContent>
                        </Card>
                    </div>
                </TabsContent>
            </Tabs>
        </div>
    </AppLayout>
</template>
