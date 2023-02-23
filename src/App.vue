<script setup>
import { useQuery } from '@vue/apollo-composable';
import gql from 'graphql-tag';
import EventList from './components/EventList.vue'

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
</script>

<template>
  <div v-if="loading">Loading...</div>
  <div v-else-if="error">{{ error.message }}</div>
  <div v-else-if="result">
    <EventList :events="result.sampleEvents" />
  </div>
</template>

<style scoped>
</style>
