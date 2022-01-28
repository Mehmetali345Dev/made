<template>
  <div class="flex flex-col space-y-3">
    <div v-for="(category, index) in documents" :key="index">
      <h1 class="text-lg font-bold text-blue-600">{{ index }}</h1>
      <div class="grid gap-1 w-full">
        <CategoryCardText
          v-for="document in category"
          :key="`document-${category}-${document.position}`"
          :document="document"
          class="w-full"
        />
      </div>
    </div>
  </div>
</template>

<script>
import groupBy from 'lodash.groupby'

export default {
  name: 'WikiExplorer',
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
