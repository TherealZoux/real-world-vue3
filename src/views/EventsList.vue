<script setup>
import EventCard from '@/components/EventCard.vue'
import EventSerevice from '@/services/EventService.js'
import { onMounted, ref } from 'vue'
const events = ref(0)
const date = new Date()
let year = date.getUTCFullYear()

onMounted(() => {
  EventSerevice.getEvents()
    .then((response) => {
      response.data[0].date = `January 28, ${year}`
      response.data[1].date = `March 14, ${year}`
      response.data[2].date = `July 22, ${year}`
      events.value = response.data
    })
    .catch((error) => {
      console.log(error)
      events.value = null
    })
})
</script>

<template>
  <div class="events">
    <h1>Events For Good</h1>
    <img v-if="events == 0" src="../assets/spin.svg" alt="" />
    <h1 v-if="events == null">404 error</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
a {
  text-decoration: none;
  color:#2c3e50;
}
</style>
