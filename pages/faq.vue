<template>
  <div class="flex flex-col w-full">
    <h1 class="text-2xl text-blue-600 font-bold">Frequently Asked Questions</h1>
    <div class="grid md:grid-cols-2 gap-3 mt-2">
      <QuestionCard
        v-for="(question, index) in questions"
        :key="index"
        :question="question"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'FaqPage',
  data() {
    return {
      questions: [
        {
          q: 'What is MADE?',
          a: 'MADE is a showcase for your dotfiles. You can find it on Github, and you can add your dotfiles to it.',
        },
        {
          q: 'How do I add my dotfiles?',
          a: 'You can add your dotfiles to MADE by fork this repository and add your .md file with your Github name, after that open pull request to me.',
        },
        {
          q: 'Is MADE open source?',
          a: 'Yes, you can find it on Github.',
        },
        {
          q: 'How I can contribute?',
          a: 'You can find contribute guidlines on Github.',
        },
        {
          q: 'Who is behind MADE?',
          a: 'Mehmet, who is also the creator of this project.',
        },
      ],
    }
  },
}
</script>

<style></style>
