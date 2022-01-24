<template>
  <div
    class="dark:text-white text-black hover:animate-spin dark:hover:animate-bounce cursor-pointer font-bold flex items-center select-none focus:outline-none rounded-xl"
    @click="switchTheme"
  >
    <h1>
      <Icon v-if="getSelectedTheme === 'light'" name="sun" class="w-5 h-5" />
      <svg
        v-else
        class="w-5 h-5"
        xmlns="http://www.w3.org/2000/svg"
        fill="currentColor"
        viewBox="0 0 256 256"
      >
        <rect width="256" height="256" fill="none"></rect>
        <path
          d="M224.3,150.3a8.1,8.1,0,0,0-7.8-5.7l-2.2.4A84,84,0,0,1,111,41.6a5.7,5.7,0,0,0,.3-1.8A7.9,7.9,0,0,0,101,31.7,100,100,0,1,0,224.3,154.9,7.2,7.2,0,0,0,224.3,150.3Z"
        ></path>
      </svg>
    </h1>
  </div>
</template>

<script>
export default {
  name: 'ColorSwitcher',
  computed: {
    /**
     * Returns the selected color mode value.
     * @returns {'light'|'dark'} The color mode as "light" or "dark".
     */
    getSelectedTheme() {
      return this.$colorMode.value
    },
  },
  methods: {
    /**
     * Updates the color mode value.
     * @param {'light'|'dark'} option The color mode option.
     */
    switchTheme() {
      this.$colorMode.preference =
        this.getSelectedTheme === 'dark' ? 'light' : 'dark'
    },
  },
}
</script>
