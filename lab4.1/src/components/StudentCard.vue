<template>
  <div class="student-card border border-gray-300 p-4 m-4 w-64 text-center mx-auto bg-white rounded-lg shadow-md hover:shadow-lg transition-transform transform hover:scale-105">
    <h3 class="text-xl font-bold text-gray-800">{{ student.name }} {{ student.surname }}</h3>
    <p class="text-gray-500 mt-2">GPA: {{ student.gpa }}</p>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'

const props = defineProps({
  student: {
    type: Object,
    required: true,
  },
})
</script>

