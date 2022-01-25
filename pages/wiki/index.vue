<template>
  <div class="flex w-full flex-col">
    <h1 class="font-bold text-blue-600 text-2xl">Hi, welcome to Wiki!</h1>
    <p class="font-bold">
      The purpose of this mini wiki is to explain what DE and WM are, to
      introduce them.
    </p>
    <h2 class="mt-2 font-bold text-xl">All documents with categories</h2>

    <div class="mt-2" v-for="(category, index) in documents" :key="index">
      <h1 class="text-lg font-bold text-blue-600">{{ index }}</h1>
      <div class="grid md:grid-cols-3 gap-3 w-full">
        <CategoryCard
          v-for="(document, index) in category"
          :key="`document-${category}-${index}}`"
          :document="document"
        />
      </div>
    </div>
  </div>
</template>

<script>
import groupBy from 'lodash.groupby'
export default {
  name: 'WikiIndex',
  data() {
    return {
      documents: [],
    }
  },
  async fetch() {
    const documents = await this.$content('wiki', { deep: true })
      .sortBy('position', 'asc')
      .without(['body', 'toc', 'dir'])
      .fetch()

    const categories = groupBy(documents, 'category')
    this.documents = categories
  },
}
</script>

<style></style>
