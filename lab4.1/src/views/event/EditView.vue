<script setup lang="ts">
import { toRefs } from 'vue'
import { type Event } from '@/types'
import { useMessageStore } from '@/stores/message1'
import { useRouter } from 'vue-router'
const props = defineProps<{
  event: Event
  id: string
}>()

const { event } = toRefs(props)
const router = useRouter()
const messageStore = useMessageStore()
const eventDetailView = () => {
  messageStore.updateMessage('Data has been updated')
  setTimeout(() => {
    messageStore.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view', params: { id: props.event.id } })
}
</script>
<template>
  <div class="edit-event-container p-6 bg-white rounded-lg shadow-md flex flex-col items-center justify-center">
    <p class="text-xl text-gray-700 mb-4">Edit event here</p>
    <button
      @click="eventDetailView"
      class="bg-red-500 text-white py-2 px-4 rounded hover:bg-gray-600 hover:shadow-lg focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2 transition-all"
    >
      Edit
    </button>
  </div>
</template>
