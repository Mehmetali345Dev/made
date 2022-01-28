<template>
  <nuxt-link
    :to="document.path"
    class="dark:bg-dark-700 p-2 rounded-md bg-gray-300 transition-all duration-500 ease-in-out hover:(bg-blue-300 dark:bg-blue-600)"
  >
    <div>
      <h1 class="line-clamp-1 font-bold">{{ document.title }}</h1>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: 'CategoryCardText',
  props: {
    document: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style></style>
