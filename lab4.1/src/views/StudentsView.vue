<template>
  <div class="students-view flex flex-wrap items-center justify-center p-6 bg-gray-100">
    <StudentCard v-for="student in students" :key="student.id" :student="student" class="m-4" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { getStudents } from '@/services/StudentService'
import StudentCard from '@/components/StudentCard.vue'

const students = ref([])

onMounted(() => {
  getStudents()
    .then(data => {
      students.value = data
    })
    .catch(error => {
      console.error('Failed to fetch students:', error)
    })
})
</script>
