<template>
  <div class="flex items-center justify-center w-full p-4">
    <div class="text-right mr-4 text-base">{{ event.category }}</div>
    <div class="text-right text-base">{{ event.organizer }}</div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<style scoped>
 .text {  
    font-size: 16px; /* 或您希望的任何大小 */  
    margin: 0 0 8px;
    border: 1px solid #000; /* 添加黑色边框 */  
    padding: 4px  
  }  
</style>
