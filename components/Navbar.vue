<template>
  <div class="md:py-8 md:px-16 p-4 w-full">
    <div class="flex justify-between items-center w-full">
      <nuxt-link
        to="/"
        class="text-3xl font-bold hover:text-blue-500 transition-all ease-in-out duration-300"
      >
        MADE
      </nuxt-link>
      <div class="font-bold text-lg flex gap-3">
        <nuxt-link
          v-for="(link, index) in links"
          :key="index"
          :to="link.url"
          class="hover:text-blue-500 transition-all ease-in-out duration-300"
          >{{ link.name }}</nuxt-link
        >
        <Color />
      </div>
    </div>
    <p class="text-gray-800 dark:text-gray-100">Mehmet's Awesome Dotfiles Explorer</p>
  </div>
</template>

<script>
export default {
  name: 'NavDefault',
  data() {
    return {
      links: [
        {
          name: 'FAQ',
          url: '/faq',
        },
        {
          name: "WM's",
          url: '/wms',
        },
        {
          name: 'Mini Wiki',
          url: '/wiki',
        },
      ],
    }
  },
}
</script>

<style></style>
