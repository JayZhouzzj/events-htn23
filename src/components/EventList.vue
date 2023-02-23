<script setup>
defineProps({
  events: {
    type: Array,
    default: () => []
  }
})

</script>

<template>
  <div class="bg-white py-24 sm:py-32">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl lg:mx-0">
        <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl text-left">Events</h2>
        <p class="mt-2 text-lg leading-8 text-gray-600 text-left">Hack the North</p>
      </div>
      <div class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-y-16 gap-x-8 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">
        <article v-for="event in events" :key="event.id" class="flex max-w-xl flex-col items-start justify-between">
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
            <a class="relative z-10 rounded-full bg-gray-50 py-1.5 px-3 font-medium text-gray-600 hover:bg-gray-100">{{ event.event_type }}</a>
          </div>
          <div class="group relative">
            <h3 class="mt-3 text-lg font-semibold leading-6 text-gray-900 group-hover:text-gray-600 text-left">
              <a :href="event.public_url">
                <span class="absolute inset-0" />
                {{ event.name }}
              </a>
            </h3>
            <p class="mt-5 text-sm leading-6 text-gray-600 line-clamp-3 text-left">{{ event.description }}</p>
          </div>
          <div class="relative mt-8 flex gap-x-4">
            <div class="text-sm leading-6">
              <p class="font-semibold text-gray-900 text-left">
                {{ event.speakers.length > 1 ? "Speakers:" : "Speaker: "}}
                <span v-for="(speaker, index) in event.speakers" :key="speaker.name">
                  <a href="#">
                    {{ speaker.name }}
                  </a>
                  <span v-if="index !== event.speakers.length - 1"> ⋅ </span>
                </span>
              </p>
              <p class="font-semibold text-gray-900 text-left">
                Related: 
                <a v-for="id in event.related_events" :key="id" class="relative z-10 rounded-full bg-gray-50 py-1.5 px-3 font-medium text-gray-600 hover:bg-gray-100">{{
                  id
                }}</a>
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