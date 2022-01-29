<template>
  <div class="flex flex-col items-center w-full">
    <div v-if="$fetchState.pending">Fetching...</div>
    <div v-else-if="$fetchState.error">An error occured</div>
    <div v-else class="w-full mt-8 gap-3">
      <h1 class="text-2xl text-blue-600 font-bold">
        Dotfiles seperated by WM/DE's
      </h1>
      <h1 class="font-bold">Selected WM/DE: {{ getQuery }}</h1>
      <div class="overflow-x-auto bar w-full flex space-x-3">
        <h1 class="font-bold sticky left-0">WM/DE's:</h1>
        <button
          v-for="(item, index) in wmDeList"
          :key="index"
          class="transition-all w-max hover:text-blue-600 duration-300 ease-in-out"
          @click="reloadList(item)"
        >
          {{ item.name }}
        </button>
      </div>
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
import list from '../assets/list.json'
export default {
  name: 'WmsPage',
  data() {
    return {
      dotfiles: [],
      number: 10,
      query: {
        name: '',
        q: '',
      },
      wmDeList: list,
    }
  },
  async fetch() {
    if (this.query.length === 0) {
      const dotfiles = await this.$content('dotfiles')
        .sortBy('createdAt', 'desc')
        .limit(this.number)
        .without(['body'])
        .fetch()
      this.dotfiles = dotfiles
    } else {
      const dotfiles = await this.$content('dotfiles')
        .where({ wm: this.query.q })
        .sortBy('createdAt', 'desc')
        .limit(this.number)
        .without(['body'])
        .fetch()
      this.dotfiles = dotfiles
    }
  },
  computed: {
    getQuery() {
      if (this.query.length === 0) {
        return 'None'
      } else {
        return this.query.name
      }
    },
  },
  methods: {
    loadMore() {
      this.number += 10
      this.$fetch()
    },
    reloadList(query) {
      this.query.q = query.query
      this.query.name = query.name
      this.$fetch()
    },
  },
}
</script>

<style lang="scss" scoped>
.bar::-webkit-scrollbar {
  display: none;
}

.bar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>
