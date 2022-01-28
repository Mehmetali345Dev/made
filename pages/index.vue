<template>
  <div class="flex flex-col items-center w-full">
    <Hero class="w-full" />
    <div v-if="$fetchState.pending">Fetching...</div>
    <div v-else-if="$fetchState.error">An error occured</div>
    <div
      v-else
      v-motion
      :initial="{
        opacity: 0,
        y: 0,
      }"
      :enter="{
        opacity: 1,
        y: 0,
        transition: {
          delay: 1300,
        },
      }"
      class="w-full mt-8 gap-3"
    >
      <h1 class="text-2xl font-bold">Look latest added dotfiles</h1>
      <div class="grid mt-2 gap-3 md:grid-cols-2">
        <DotfileCard
          v-for="(dotfile, index) in dotfiles"
          :key="`dotfile-${index}`"
          :dotfile="dotfile"
        />
      </div>
      <button
        v-if="dotfiles.length >= number"
        class="text-xl font-bold justify-center items-center w-full bg-transparent mt-4 flex gap-3"
        @click="loadMore()"
      >
        <Icon name="arrow-down" class="animate-bounce w-6 h-6" />Load More
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      dotfiles: [],
      number: 10,
    }
  },
  fetchOnServer: false,
  async fetch() {
    const dotfiles = await this.$content('dotfiles')
      .sortBy('createdAt', 'desc')
      .limit(this.number)
      .without(['body'])
      .fetch()

    this.dotfiles = dotfiles
  },
  methods: {
    loadMore() {
      this.number += 10
      this.$fetch()
    },
  },
}
</script>
