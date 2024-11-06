<template>
  <div class="container mx-auto p-6">

    <h1 class="text-3xl font-bold text-gray-900 mb-6">Events For Good</h1>
    <div class="page-size-selector mb-6">
      <label for="pageSize" class="block text-gray-700">Events per page:</label>
      <select id="pageSize" v-model="pageSize" @change="updateRoute(Number(pageSize))"
        class="border border-gray-300 p-2 w-24 rounded">
        <option value="3">default</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
      </select>
    </div>
    <div class="flex flex-col items-center">
      <div v-for="event in events" :key="event.id">
        <EventCard :event="event" />
        <EventInfo :event="event" />
      </div>
      <div class="pagination flex w-full md:w-4/5 justify-between mt-6">
        <RouterLink id="page-prev" :to="{
          name: 'event-list-view',
          query: { page: page - 1, size: pageSize },
        }" rel="prev" v-if="page !== 1" class="text-left text-blue-500 hover:underline">&lt; Prev Page</RouterLink>
        <RouterLink id="page-next" :to="{
          name: 'event-list-view',
          query: { page: page + 1, size: pageSize },
        }" rel="next" v-if="hasNextPage" class="text-right text-blue-500 hover:underline">Next Page &gt;
        </RouterLink>
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventInfo from '@/EventCG.vue'
import type { Event } from '@/types'
import { useRoute, useRouter } from 'vue-router'
import { ref, onMounted, computed, watchEffect } from 'vue'
import EventService from '@/services/EventService'

const pageSize = ref<number | string>(2)
const route = useRoute()
const router = useRouter()
const updateRoute = (newSize: number) => {
  router.push({
    name: route.name,
    query: { ...route.query, size: newSize },
  })
}
const events = ref<Event[] | null>(null)
const totalEvents = ref(0)
const hasNexPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / 3)
  return page.value < totalPages
})

const props = defineProps({
  page: {
    type: Number,
    required: true,
  },
  size: {
    type: Number,
    required: true,
    default: 2,
  },
})
const page = computed(() => props.page)
const size = computed(() => props.size)

onMounted(() => {
  watchEffect(() => {
    EventService.getEvents(size.value, page.value)
      .then(response => {
        events.value = response.data
        totalEvents.value = response.headers['x-total-count']
      })
      .catch(error => {
        console.error('There was an error!', error)
      })
  })
})
</script>


<style scoped>
/*
 .event-info {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 10px;
}
.event-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80%;
  padding: 10px;
  margin: 10px auto;
}
.category,
.organizer {
  font-size: 16px;
  margin-left: 8px;
  text-align: center;
}
.pagination {
  display: flex;
  width: 290px;

}
.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
  */
</style>
