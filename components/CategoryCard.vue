<template>
  <nuxt-link
    :to="document.path"
    class="dark:bg-dark-700 p-4 rounded-md bg-gray-300 transition-all duration-500 ease-in-out hover:(bg-blue-300 dark:bg-blue-600)"
  >
    <div>
      <h1 class="text-lg font-bold">{{ document.title }}</h1>
      <p>{{ document.desc }}</p>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: 'CategoryCard',
  props: {
    document: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style></style>
