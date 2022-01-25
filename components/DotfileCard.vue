<template>
  <nuxt-link
    to="/faq"
    class="flex flex-col w-full justify-between rounded-t-md transition-all ease-in-out duration-300 hover:(dark:bg-dark-700 bg-gray-300)"
  >
    <Skeleton type="image" :imageUrl="dotfile.screenshots[0]" class="rounded-t-md h-full max-h-64" />
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
