<script setup lang="ts">
import { ref, onMounted } from 'vue'
import PassengerCard from '@/components/PassengerCard.vue'
import PassengerService from '@/services/PassengerService'

const passengers = ref([])

onMounted(async () => {
  try {
    const response = await PassengerService.getPassengers()
    passengers.value = response.data.data
  } catch (error) {
    console.error('Failed to fetch passengers', error)
  }
})
</script>

<template>
  <div class="events">
    <div v-for="passenger in passengers" :key="passenger._id">
      <PassengerCard :passenger="passenger" />
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
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
</style>
