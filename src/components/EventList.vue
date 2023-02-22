<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)

const events = [
  {
    "id": 1,
    "name": "Vonage API Workshop",
    "event_type": "workshop",
    "permission": "private",
    "start_time": 1610442000000,
    "end_time": 1610443800000,
    "description": "A Nanoleaf Shapes Mini Triangle Smarter Kit will be awarded to each member of the winning team for Best Use of Vonage API. Vonage is a cloud communications platform that allows developers to integrate voice, video and messaging into their applications using their communication APIs. So whether you want to build video calls into your app, create a Facebook bot, or build applications on top of programmable phone numbers, Vonage has got you covered",
    "speakers": [
      {
        "name": "Vonage"
      }
    ],
    "public_url": "",
    "private_url": "https://hopin.com/events/hack-the-north-2020",
    "related_events": [
      2,
      3
    ]
  },
  {
    "id": 2,
    "name": "Rapid Prototyping with Flutter and Firebase",
    "event_type": "tech_talk",
    "permission": "public",
    "start_time": 1610442000000,
    "end_time": 1610447400000,
    "description": "Ever need to make an app quickly, such as for a hackathon or prototype, but not know where to start? In this talk you will learn about Flutter, Google's cross-OS development platform, as well as Firebase, Google's Backend as a Service (BaaS) platform, and how they can be used to quickly take your ideas and turn them into beautiful and functional prototypes. We will discuss multiple useful widgets, third-party plugins, and how to implement various features of Firebase that can support your users. This talk will cover code implementations as well as theory.",
    "speakers": [
      {
        "name": "Firebase"
      }
    ],
    "public_url": "https://youtu.be/rgfezE92mog",
    "private_url": "https://hopin.com/events/hack-the-north-2020",
    "related_events": [
      1,
      3
    ]
  },
  {
    "id": 3,
    "name": "Microsoft API Workshop",
    "event_type": "workshop",
    "permission": "public",
    "start_time": 1610449200000,
    "end_time": 1610452800000,
    "description": "The Azure prize is awarded to the team who makes the best use of Azure during this hackathon. The primary requirement is that your hack project includes Azure in some way.",
    "speakers": [
      {
        "name": "Microsoft"
      }
    ],
    "public_url": "https://youtu.be/M3GQs6fEjs4",
    "private_url": "https://hopin.com/events/hack-the-north-2020",
    "related_events": [
      1,
      2,
      4
    ]
  },
  {
    "id": 4,
    "name": "Hootsuite API Workshop",
    "event_type": "workshop",
    "permission": "public",
    "start_time": 1610449200000,
    "end_time": 1610451000000,
    "description": "A Raspberry Pi 4 will be awarded to each member of the winning team who makes the best use of the Hootsuite API to improve how we communicate in today's connected world.",
    "speakers": [
      {
        "name": "Hootsuite"
      }
    ],
    "public_url": "https://youtu.be/lJ4uGA176HY",
    "private_url": "https://hopin.com/events/hack-the-north-2020",
    "related_events": [
      2,
      3,
      5
    ]
  },
]

const posts = [
  
  // More posts...
]
</script>

<template>
  <div class="bg-white py-24 sm:py-32">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl lg:mx-0">
        <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">Events</h2>
        <p class="mt-2 text-lg leading-8 text-gray-600">Hack the North</p>
      </div>
      <div class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-y-16 gap-x-8 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">
        <article v-for="post in posts" :key="post.id" class="flex max-w-xl flex-col items-start justify-between">
          <div class="flex items-center gap-x-4 text-xs">
            <time :datetime="post.datetime" class="text-gray-500">{{ post.date }}</time>
            <a :href="post.category.href" class="relative z-10 rounded-full bg-gray-50 py-1.5 px-3 font-medium text-gray-600 hover:bg-gray-100">{{ post.category.title }}</a>
          </div>
          <div class="group relative">
            <h3 class="mt-3 text-lg font-semibold leading-6 text-gray-900 group-hover:text-gray-600">
              <a :href="post.href">
                <span class="absolute inset-0" />
                {{ post.title }}
              </a>
            </h3>
            <p class="mt-5 text-sm leading-6 text-gray-600 line-clamp-3">{{ post.description }}</p>
          </div>
          <div class="relative mt-8 flex items-center gap-x-4">
            <img :src="post.author.imageUrl" alt="" class="h-10 w-10 rounded-full bg-gray-50" />
            <div class="text-sm leading-6">
              <p class="font-semibold text-gray-900">
                <a :href="post.author.href">
                  <span class="absolute inset-0" />
                  {{ post.author.name }}
                </a>
              </p>
              <p class="text-gray-600">{{ post.author.role }}</p>
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
