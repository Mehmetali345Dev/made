<template>
  <div class="flex flex-col w-full gap-3">
    <header class="space-y-3">
      <h1 class="text-2xl font-bold text-blue-600">{{ document.title }}</h1>
      <p>{{ document.desc }}</p>
      <div class="font-bold text-sm flex gap-3">
        <div class="flex gap-1 items-center">
          <Icon name="calendar" class="w-5 h-5" />{{ getCreateDate }}
        </div>
        <div class="flex gap-1">
          <Icon name="clock-clockwise" class="w-5 h-5" />{{ getUpdateDate }}
        </div>
      </div>
      <div class="w-full h-1 bg-blue-600"></div>
    </header>
    <article class="w-full">
      <nuxt-content :document="document" />
    </article>
    <div class="flex w-full justify-between">
      <nuxt-link
        v-if="other.prev !== null"
        class="p-4 bg-gray-400 rounded-md w-max dark:bg-dark-700"
        :to="other.prev.path"
      >
        <h1
          class="font-bold line-clamp-1 transition-all ease-in-out hover:text-blue-600 duration-300"
        >
          Prev: {{ other.prev.title }}
        </h1>
        <p>{{ other.prev.category }}</p>
      </nuxt-link>
      <nuxt-link
        v-if="other.next !== null"
        class="p-4 bg-gray-400 rounded-md w-max dark:bg-dark-700"
        :to="other.next.path"
      >
        <h1
          class="font-bold transition-all line-clamp-1 ease-in-out hover:text-blue-600 duration-300"
        >
          Next: {{ other.next.title }}
        </h1>
        <p>{{ other.next.category }}</p>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WikiSlug',
  data() {
    return {
      document: [],
      other: {
        prev: null,
        next: null,
      },
    }
  },
  async fetch() {
    const path = `/wiki/${this.$route.params.pathMatch}` || 'index'

    const [document] = await this.$content('wiki', { deep: true })
      .where({ path })
      .fetch()
    this.document = document

    const [prev, next] = await this.$content('wiki', { deep: true })
      .only(['category', 'title', 'path', 'to'])
      .sortBy('position', 'asc')
      .where({ category: document.category })
      .surround(document.path)
      .fetch()

    this.other = {
      prev: prev || null,
      next: next || null,
    }
  },
  computed: {
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
