<template>
  <nuxt-link
    :to="{
      name: 'dotfiles-slug',
      params: { slug: dotfile.slug },
    }"
    class="flex flex-col w-full justify-between rounded-t-md transition-all ease-in-out duration-300 hover:(dark:bg-dark-700 bg-gray-300)"
  >
    <Skeleton
      class="rounded-t-md h-full max-h-64"
      type="image"
      :image-url="getimageUrl"
    />
    <div class="flex flex-col p-4 gap-1 justify-center">
      <h1 class="font-bold text-lg">{{ dotfile.title }}</h1>
      <p>{{ dotfile.desc }}</p>
      <h2 class="font-bold">
        WM/DE: <span class="text-blue-600">{{ dotfile.wm }}</span>
      </h2>
      <div class="flex gap-1">
        <Icon name="user-circle" class="w-5 h-5" />{{ dotfile.username }}
      </div>
      <div class="flex gap-1 items-center">
        <Icon name="calendar" class="w-5 h-5" />{{ getCreateDate }}
      </div>
      <div class="flex gap-1">
        <Icon name="clock-clockwise" class="w-5 h-5" />{{ getUpdateDate }}
      </div>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: 'DotfileCard',
  props: {
    dotfile: {
      type: Object,
      required: true,
    },
  },
  computed: {
    getimageUrl() {
      if (this.dotfile?.screenshots.length > 0) {
        return this.dotfile.screenshots[0]
      } else {
        return ''
      }
    },
    getCreateDate() {
      const now = this.$moment()
      const createdAt = this.$moment(this.dotfile.createdAt)
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
      const updatedAt = this.$moment(this.dotfile.updatedAt)
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
