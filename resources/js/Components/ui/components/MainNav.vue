<script setup lang="ts">
import { cn } from '@/lib/utils'
import { Link } from '@inertiajs/vue3';
</script>

<template>
  <nav
    :class="cn('flex items-center space-x-4 lg:space-x-6', $attrs.class ?? '')"
  >
    <Link
      :href="route('dashboard')"cal
      class="text-sm font-medium transition-colors hover:text-primary"
    >
      {{ $t('Dashboard') }}
    </Link>
  </nav>
</template>
