<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService.js'

const props = defineProps({
  id: {
    required: true
  }
})

const event = ref(null)
const date = new Date()
let year = date.getUTCFullYear()
onMounted(() => {
  EventService.getEvent(props.id)
    .then((response) => {
      response.data.date = `January 28, ${year}`
      event.value = response.data
    })
    .catch((error) => {
      console.log(error)
    })
})
</script>

<template>
  <img v-if="!event" src="../assets/spin.svg" alt="" />

  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>
