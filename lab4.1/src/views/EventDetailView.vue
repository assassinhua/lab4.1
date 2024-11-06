<script setup lang="ts">
import { ref, onMounted, defineProps } from 'vue'
import type { Event } from '@/types'
import EventService from '@/services/EventService'
const event = ref<Event | null>(null)
const props = defineProps({
  id: {
    type: String,
    required: true,
  },
})

onMounted(() => {
  EventService.getEvent(parseInt(props.id))
    .then(response => {
      event.value = response.data
    })
    .catch(error => {
      console.error('There was an error!', error)
    })
})
</script>
<template>
  <div v-if="event" class="event-details max-w-3xl mx-auto p-6 bg-white rounded-lg shadow-md mt-8">
    <h1 class="text-3xl font-bold text-gray-900 mb-4">{{ event.title }}</h1>
    <p class="text-gray-700 mb-4">{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p class="text-gray-600">{{ event.description }}</p>
  </div>
</template>