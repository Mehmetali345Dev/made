<template>
  <div v-if="$fetchState.pending">Fetching...</div>
  <div v-else-if="$fetchState.error">
    An error occured or this user doesn't added dotfile
  </div>
  <div v-else class="flex flex-col w-full gap-3">
    <header class="space-y-3">
      <nuxt-link class="text-blue-600 font-bold" to="/">Go Home</nuxt-link>
      <Skeleton
        type="image"
        :image-url="document.screenshots[0]"
        class="rounded-t-md"
      />
      <h1 class="text-2xl font-bold text-blue-600">{{ document.title }}</h1>
      <p>{{ document.desc }}</p>
      <div
        class="font-bold items-center text-sm md:flex grid grid-cols-2 gap-3"
      >
        <div class="flex gap-1">
          <Icon name="user-circle" class="w-5 h-5" />{{ document.username }}
        </div>
        <div class="flex gap-1 items-center">
          <Icon name="calendar" class="w-5 h-5" />{{ getCreateDate }}
        </div>
        <div class="flex gap-1">
          <Icon name="clock-clockwise" class="w-5 h-5" />{{ getUpdateDate }}
        </div>
        <a
          target="_blank"
          rel="noopener noreferrer"
          :href="`https://github.com/${document.slug}/dotfiles`"
          class="px-6 flex gap-3 py-2 dark:bg-gray-50 items-center dark:text-black text-white rounded-md bg-dark-800"
        >
          <Icon name="github" class="w-5 h-5" />View on Github</a
        >
      </div>
    </header>
    <article class="w-full">
      <nuxt-content :document="document" />
    </article>
    <div v-if="getScreenshots.length >= 1">
      <h1 class="text-2xl font-bold text-blue-600 mb-2">Other Screenshots</h1>
      <div class="grid md:grid-cols-2 gap-3">
        <a
          v-for="index in getScreenshots"
          :key="`screenshot-${index}`"
          :href="index"
          target="_blank"
          rel="noopener noreferrer"
          title="Click to see screenshot"
        >
          <Skeleton type="image" :image-url="index" class="rounded-md" />
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DotfileSlug',
  data() {
    return {
      document: [],
    }
  },
  async fetch() {
    const post = await this.$content("dotfiles", this.$route.params.slug).fetch()
    this.document = post
  },
  computed: {
    getScreenshots() {
      return this.document.screenshots?.slice(1)
    },
    getCreateDate() {
      const now = this.$moment()
      const createdAt = this.$moment(this.document.createdAt)
      const diff = now.diff(createdAt, 'days')
      if (diff === 0) return 'Today'
      else if (diff === 1) return 'Yesterday'
      else if (diff <= 30) return `${diff} days ago`
      else if (diff >= 30 && diff <= 90)
        return `${Math.floor(diff / 30)} month(s) ago`
      else return createdAt.format('DD/MM/YYYY')
    },
    getUpdateDate() {
      const now = this.$moment()
      const updatedAt = this.$moment(this.document.updatedAt)
      const diff = now.diff(updatedAt, 'days')
      if (diff === 0) return 'Today'
      else if (diff === 1) return 'Yesterday'
      else if (diff <= 30) return `${diff} days ago`
      else if (diff >= 30 && diff <= 90)
        return `${Math.floor(diff / 30)} month(s) ago`
      else return updatedAt.format('DD/MM/YYYY')
    },
  },
}
</script>

<style></style>
