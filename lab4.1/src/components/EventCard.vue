<script setup lang="ts">
import type { Event } from '@/types'
defineProps<{
  event: Event
}>()
</script>

<template>
  <RouterLink
    class="event-link block w-full max-w-md text-center bg-white rounded-lg shadow-md hover:shadow-lg transition-transform transform hover:scale-105"
    :to="{ name: 'event-detail-view', params: { id: event.id } }"
  >
    <div class="p-6">
      <h2 class="text-2xl font-bold text-gray-800 mb-2">{{ event.title }}</h2>
      <span class="block text-gray-500 text-sm">@{{ event.time }} on {{ event.date }}</span>
    </div>
  </RouterLink>
</template>

<style scoped>
.event-link {
  text-decoration: none;
  color: #2c3e50;
}
</style>