<script setup lang="ts">
import { toRefs } from 'vue'
import { type Event } from '@/types'
import { useMessageStore } from '@/stores/message'
import { useRouter } from 'vue-router'
const props = defineProps<{
  event: Event
  id: string
}>()

const { event } = toRefs(props)
const router = useRouter()
const store = useMessageStore()
const register = () => {
  store.updateMessage(
    'You are successuflly registered for ' + props.event.title,
  )
  setTimeout(() => {
    store.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view', params: { id: props.event.id } })
}
</script>
<template>
  <div class="register-event-container p-6 bg-white rounded-lg shadow-md flex flex-col items-center justify-center">
    <p class="text-xl text-gray-700 mb-4">Register event here</p>
    <button
      @click="register"
      class="bg-yellow-500 text-white py-2 px-4 rounded hover:bg-gray-300 hover:shadow-lg focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2 transition-all"
    >
      Register
    </button>
  </div>
</template>
