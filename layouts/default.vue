<template>
  <div
    class="flex flex-col items-center dark:bg-dark-900 text-black dark:text-white bg-gray-100 min-h-screen"
  >
    <Navbar />
    <div class="flex-grow flex justify-center w-11/12 md:py-8 md:px-16 p-4">
      <Nuxt class="w-11/12 flex-grow" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout',
}
</script>

<style></style>
