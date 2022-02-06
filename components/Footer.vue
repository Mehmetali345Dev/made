<template>
  <div class="md:py-8 md:px-16 p-4 w-full">
    <div class="md:flex gap-3 justify-between items-center w-full">
      <a
        to="https://345dev.me"
        class="text-lg font-bold hover:text-blue-500 transition-all ease-in-out duration-300"
      >
        Made by Mehmetali345Dev
      </a>
      <div class="font-bold text-lg flex gap-3">
        <a
          to="https://github.com/mehmetali345dev/made"
          class="text-lg font-bold hover:text-blue-500 transition-all ease-in-out duration-300"
        >
          View on Github
        </a>
        <Color />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FooterDefault',
}
</script>

<style></style>
