<script setup>
import { useQuery } from '@vue/apollo-composable';
import gql from 'graphql-tag';
import EventList from './components/EventList.vue'
import { ref } from 'vue'

const loggedIn = ref(false)
const eventList = ref()

const EVENTS_QUERY = gql`
  query {
    sampleEvents {
      id
      name
      event_type
      permission
      start_time
      end_time
      description
      speakers {
        name
      }
      public_url
      private_url
      related_events
    }
  }
`

const { result, loading, error } = useQuery(EVENTS_QUERY)

function toggleLogin() {
  // Let everyone log in for the moment.
  loggedIn.value = !loggedIn.value
  eventList.value.openModal()
}
</script>

<template>
  <div class="flex justify-end items-center h-16">
    <button @click="toggleLogin" class="px-4 py-2 font-medium text-white bg-indigo-500 rounded-md hover:bg-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-50">
      {{loggedIn ? "Log out" : "Log in"}}
    </button>
  </div>
  <div v-if="loading">Loading...</div>
  <div v-else-if="error">{{ error.message }}</div>
  <div v-else-if="result">
    <EventList 
      :events="loggedIn ? result.sampleEvents : result.sampleEvents.filter(e => e.public_url)" 
      :loggedIn="loggedIn"
      ref="eventList"
    />
  </div>
</template>

<style scoped>
</style>
