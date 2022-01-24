<template>
  <div class="flex flex-col items-center w-full">
    <Hero class="w-full" />
    <div class="w-full mt-8 gap-3">
      <h1 class="text-2xl font-bold">Look latest added dotfiles</h1>
      <div class="grid mt-2 md:grid-cols-2">
        <DotfileCard
          v-for="(dotfile, index) in dotfiles"
          :key="`dotfile-${index}`"
          :dotfile="dotfile"
        />
      </div>
      <button
        v-if="dotfiles.length >= 10"
        @click="loadMore()"
        class="text-xl font-bold justify-center items-center w-full bg-transparent mt-2 flex gap-3"
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
  async fetch() {
    const dotfiles = await this.$content()
      .sortBy('date', 'desc')
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
