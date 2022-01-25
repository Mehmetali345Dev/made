<template>
  <div>{{ document }}</div>
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
}
</script>

<style></style>
