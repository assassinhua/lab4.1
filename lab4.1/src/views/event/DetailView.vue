<script setup lang="ts">
import { toRefs, defineProps } from 'vue'
import type { Event } from '@/types'

const props = defineProps<{
  event: Event
  id: string
}>()
const { event } = toRefs(props)
</script>
<template>
  <div class="event-details p-6 bg-white rounded-lg shadow-md transition-transform transform hover:scale-105 hover:shadow-lg">
    <p class="text-lg text-gray-700 mb-4">
      {{ event.time }} on {{ event.date }} @ {{ event.location }}
    </p>
    <p class="text-gray-600">{{ event.description }}</p>
  </div>
</template>
