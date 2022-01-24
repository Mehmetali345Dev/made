<template>
  <nuxt-link to="/" class="flex flex-col w-full rounded-t-md dark:bg-dark-700">
    <img :src="dotfile.screenshots[0]" class="w-full rounded-t-md" alt="" />
    <div class="flex flex-col p-4 gap-1 justify-center">
      <h1 class="font-bold text-lg">{{ dotfile.title }}</h1>
      <p>{{ dotfile.desc }}</p>
      <h2 class="font-bold">
        WM/DE: <span class="text-blue-600">{{ dotfile.wm }}</span>
      </h2>
      <h2 class="font-bold">
        Date: <span class="text-blue-600">{{ dotfile.date }}</span>
      </h2>
      <h3 class="font-bold">
        Author: <span class="text-blue-600">{{ dotfile.username }}</span>
      </h3>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: 'DotfileCard',
  props: {
    dotfile: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style></style>
