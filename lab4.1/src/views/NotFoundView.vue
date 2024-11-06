<script setup lang="ts">
import { defineProps, withDefaults } from 'vue'
const props = withDefaults(
  defineProps<{
    resource: string
  }>(),
  {
    resource: 'page',
  },
)
</script>
<template>
  <div class="error-page flex flex-col items-center justify-center min-h-screen bg-gray-100 text-center">
    <h1 class="text-4xl font-bold text-red-500 mb-4">Oops!</h1>
    <h3 class="text-xl text-gray-700 mb-6">
      The {{ props.resource }} you're looking for is not here.
    </h3>
    <router-link :to="{ name: 'event-list-view' }" class="text-blue-500 underline hover:text-blue-700">Back to the home
      page</router-link>
  </div>
</template>
