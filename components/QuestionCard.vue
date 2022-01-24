<template>
  <div
    class="bg-gradient-to-r from-blue-600 to-green-600 rounded-md shadow-md shadow-gray-600 p-4 flex flex-col gap-3"
  >
    <h1 class="text-xl font-bold">Question: "{{ question.q }}"</h1>
    <p class="text-lg">Answer: "{{ question.a }}"</p>
  </div>
</template>

<script>
export default {
  name: 'QuestionCard',
  props: {
    question: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style></style>
