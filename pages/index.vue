<template>
  <div>
    <h1>Events</h1>

    <EventCard v-for="(event, index) in events" :key="index" :event="event" />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '~/components/EventCard.vue'

export default {
  components: {
    EventCard
  },
  async fetch (context) {
    try {
      await context.store.dispatch('events/fetchEvents')
    } catch (e) {
      context.error({ statusCode: 503, message: 'Unable to fetch events at this time, please try again later.' })
    }
  },
  head () {
    return {
      title: 'Event listing'
    }
  },
  computed: {
    ...mapState({ events: state => state.events.events })
  }
}
</script>
