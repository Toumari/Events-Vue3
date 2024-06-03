<script setup>

import { ref, onMounted } from 'vue';
import EventService from '@/services/EventService.js';
import EventCard from '@/components/EventCard.vue';

onMounted(async () => {
  const response = await EventService.getEvents();
  events.value = response.data;
});


const events = ref(null)

</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
