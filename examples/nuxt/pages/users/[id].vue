<script lang="ts">
import { defineBasicLoader } from 'unplugin-vue-router/data-loaders/basic'
const delay = (ms: number) => new Promise((resolve) => setTimeout(resolve, ms))

export const useUserData = defineBasicLoader(
  async (route) => {
    await delay(300)
    const user = {
      id: route.params.id,
      when: Date.now(),
      n: Math.round(Math.random() * 10000),
      name: 'John Doe',
    }
    console.log('fetching user:')
    console.table(user)
    return user
  },
  { key: 'user' }
)
</script>

<script setup lang="ts">
const { data: user } = useUserData()
</script>

<template>
  <div>
    <h1>User {{ $route.params.id }}</h1>
    <pre>{{ user }}</pre>
  </div>
</template>
