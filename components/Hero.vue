<template>
  <div class="w-full">
    <div class="items-center w-full">
      <h1
        class="text-4xl font-bold text-blue-600"
        v-motion
        :initial="{
          opacity: 0,
          y: 100,
        }"
        :enter="{
          opacity: 1,
          y: 0,
          transition: {
            delay: 500,
          },
        }"
      >
        MADE
      </h1>
      <p
        v-motion
        :initial="{
          opacity: 0,
          x: 100,
        }"
        :enter="{
          opacity: 1,
          x: 0,
          transition: {
            delay: 700,
          },
        }"
        class="w-full md:w-3/6"
      >
        MADE is awesome showcase for your dotfiles! Just fork this and add your
        .md file with your Github name, after that open pull request to me.
      </p>
    </div>
    <div
      class="flex mt-2"
      v-motion
      :initial="{
        opacity: 0,
        y: 100,
      }"
      :enter="{
        opacity: 1,
        y: 0,
        transition: {
          delay: 1000,
        },
      }"
    >
      <a
        target="_blank"
        rel="noopener noreferrer"
        href="https://github.com/mehmetali345dev/made"
        class="px-6 flex gap-3 py-2 dark:bg-gray-50 dark:text-black text-white rounded-md bg-dark-800"
      >
        <Icon name="github" class="w-6 h-6" />View on Github</a
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexHero',
}
</script>

<style></style>
