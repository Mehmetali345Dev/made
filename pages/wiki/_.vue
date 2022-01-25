<template>
  <div>{{ wut }}</div>
</template>

<script>
export default {
  name: 'WikiIndex',
  middleware({ app, params, redirect }) {
    console.log(params.pathMatch);
    if (params.pathMatch === '/') {
      redirect(app.localePath('/wiki/'))
    }
  },
  async fetch() {
    const path = `/wiki/${this.$route.params.pathMatch || 'index'}`
    const [document] = await this.$content({ deep: true })
      .where({ path })
      .fetch()
    this.wut = document
  },
  data() {
    return {
      wut: [],
    }
  },
}
</script>

<style></style>
