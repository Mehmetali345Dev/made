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
  </div>
</template>

<script>
export default {
  name: 'WikiSlug',
  data() {
    return {
      document: [],
    }
  },
  async fetch() {
    const path = `/wiki/${this.$route.params.pathMatch || 'index'}`
    const [document] = await this.$content({ deep: true })
      .where({ path })
      .fetch()
    this.document = document
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
