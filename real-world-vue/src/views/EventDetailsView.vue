<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService.js'

const props = defineProps({
    id: {
        type: String,
        required: true
    }
})

const event = ref(null);


onMounted(() => {
    // fetch event (by id) and set local event data
    EventService.getEvent(props.id)
        .then(response => {
            event.value = response.data
        })
        .catch(error => {
            console.error('There was an error:', error.response)
        })
})
</script>

<template>
    <div v-if="event">
        <h1>{{ event.title }}</h1>
        <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
        <p>{{ event.description }}</p>
    </div>
</template>