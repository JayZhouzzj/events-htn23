<script setup>
import { ref, reactive, computed } from 'vue'
import LogInModal from './LogInModal.vue'

const openLogInModal = ref(false)

const props = defineProps({
  events: {
    type: Array,
    default: () => []
  },
  loggedIn: {
    type: Boolean,
    default: false
  }
})

const sortedEvents = computed(() => {
  return props.events.slice().sort((a, b) => (a.start_time - b.start_time))
})

const eventsMap = computed(() => {
  return props.events.reduce((acc, curr) => {
    acc[curr.id] = curr
    return acc
  }, {})
})

function getEvent(id) {
  return this.eventsMap[id]
}

function openModal() {
  openLogInModal.value = true
}

defineExpose({
  openModal
})

</script>

<template>
  <div class="bg-white py-24 sm:py-32">  
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <LogInModal :open="openLogInModal" @close="openLogInModal = false"/>
      <div class="mx-auto max-w-2xl lg:mx-0">
        <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl text-left">Events</h2>
        <p class="mt-2 text-lg leading-8 text-gray-600 text-left">Hack the North</p>
      </div>
      <div class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-y-16 gap-x-8 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">
        <article v-for="event in sortedEvents" :key="event.id" class="flex max-w-xl flex-col items-start justify-start">
          <div class="flex items-center gap-x-4 text-xs">
            <time :datetime="event.start_time" class="text-gray-500">{{ 
              new Date(event.start_time).toLocaleTimeString(undefined, {
                hour: '2-digit', minute: '2-digit'
              })
              + " - " +
              new Date(event.end_time).toLocaleTimeString(undefined, {
                hour: '2-digit', minute: '2-digit'
              }) + ", " +
              new Date(event.start_time).toLocaleDateString()
            }}
            </time>
            <a rel="noopener noreferrer" target="_blank" class="relative z-10 rounded-full bg-gray-50 py-1.5 px-3 font-medium text-gray-600 hover:bg-gray-100">{{ event.event_type }}</a>
          </div>
          <div class="group relative">
            <h3 class="mt-3 text-lg font-semibold leading-6 text-gray-900 group-hover:text-gray-600 text-left">
              <a :href="loggedIn ? event.private_url : event.public_url" rel="noopener noreferrer" target="_blank">
                <span class="absolute inset-0" />
                {{ event.name }}
              </a>
            </h3>
            <p class="mt-5 text-sm leading-6 text-gray-600 line-clamp-3 text-left">{{ event.description }}</p>
          </div>
          <div class="relative flex gap-x-4">
            <div class="mt-5 text-sm leading-6">
              <p class="font-semibold text-gray-900 text-left">
                {{ event.speakers.length > 1 ? "Speakers:" : "Speaker: "}}
                <span v-for="(speaker, index) in event.speakers" :key="speaker.name">
                  <a :href="'https://www.google.com/search?q=' + speaker.name" rel="noopener noreferrer" target="_blank">
                    {{ speaker.name }}
                  </a>
                  <span v-if="index !== event.speakers.length - 1"> ⋅ </span>
                </span>
              </p>
              <p class="font-semibold text-gray-900 text-left">
                Related: 
                <br />
                <span v-for="id in event.related_events" :key="id" class="text-left">
                  <a v-if="getEvent(id)" :href="loggedIn ? getEvent(id).private_url : getEvent(id).public_url" class="relative z-10 inline-block rounded-full bg-gray-50 py-1.5 px-3 font-medium text-gray-600 hover:bg-gray-100 text-ellipsis ml-0 mr-2 my-0.5 text-xs" rel="noopener noreferrer" target="_blank">{{
                    getEvent(id).name
                  }}</a>
                </span>
              </p>
            </div>
          </div>
        </article>
      </div>
    </div>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
