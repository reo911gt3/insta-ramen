<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <div id="nav">
      <router-link :to="{ name: 'EventDetails', params: { id } }"
        >Details</router-link
      >
      <router-link :to="{ name: 'EventRegister', params: { id } }"
        >Register</router-link
      >
      <router-link :to="{ name: 'EventEdit', params: { id } }"
        >Edit</router-link
      >
    </div>
    <p>Register for event here</p>
  </div>
</template>

<script>
import EventService from "../../services/EventServices";

export default {
  props: ['id'],
  data() {
    return {
      event: null,
    }
  },
  created() {
    // fetch event (by id) and set local event data
    EventService.getEvent(this.id)
    .then(
          response => {
            this.event = response.data
          }
      )
        .catch(error => {
          console.log(error)
        })
  }
}
</script>