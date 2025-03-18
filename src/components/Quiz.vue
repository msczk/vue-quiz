<script setup>
  import Progress from '@/components/Progress.vue'
  import { computed, ref } from 'vue'
  import Question from '@/components/Question.vue'
  import Recap from '@/components/Recap.vue'

  const props = defineProps({
    quiz: Object
  })

  const step = ref(0)

  const state = ref('questions')

  const answers = ref(props.quiz.questions.map(() => null));

  const question = computed(() => props.quiz.questions[step.value])

  const addAnswer = (answer) => {
    answers.value[step.value] = answer

    if(step.value === props.quiz.questions.length - 1)
    {
      state.value = 'recap'
    }else{
      step.value++
    }
  }

  const restartQuiz = () => {
    answers.value = props.quiz.questions.map(() => null)
    step.value = 0
    state.value = 'questions'
  }

</script>

<template>
  <h1>
    {{quiz.title}}
  </h1>

  <Progress v-if="state === 'questions'" :step="step" :total="quiz.questions.length" />

  <Question v-if="state === 'questions'" :question="question" @answer="addAnswer" :key="question.question" />

  <Recap v-if="state === 'recap'" :quiz="quiz" :answers="answers" @restart="restartQuiz" />

</template>

<style scoped>
h1{
  text-align: center;
  margin-top: 10px;
}
</style>