<template>
  <div
    class="flex transition-all flex-col items-center dark:bg-dark-900 text-black dark:text-white bg-gray-100 min-h-screen"
  >
    <Navbar />
    <WikiExplorer v-if="$route.params.pathMatch" class="md:hidden" />
    <div
      class="flex-grow flex justify-center items-start w-11/12 gap-3 md:py-8 md:px-16 p-4"
    >
      <div class="w-11/12">
        <WikiExplorer
          v-if="$route.params.pathMatch"
          class="hidden md:block min-w-48"
        />
        <Nuxt />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout',
}
</script>

<style></style>
