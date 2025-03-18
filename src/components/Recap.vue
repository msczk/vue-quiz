<script setup>
  import { computed } from 'vue'

  const props = defineProps({
    quiz: Object,
    answers: Array
  })

  const score = computed(() => {
    let score = 0
    props.answers.map((answer, index) => {
      if(answer === props.quiz.questions[index].correct_answer)
      {
        score++;
      }
    })

    return score
  })

  const emits = defineEmits(['restart'])
</script>

<template>
  <p v-if="score >= quiz.minimum_score">
    {{quiz.success_message}}
  </p>
  <p v-else>
    {{quiz.failure_message}}
  </p>
  <p>
    Votre score {{score}}/{{quiz.questions.length}}
  </p>
  <div>
    <button @click="emits('restart')">Recommencer</button>
  </div>
</template>

<style scoped>
  p,
  div{
    text-align: center;
  }
</style>