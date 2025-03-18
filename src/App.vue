<script setup>
import { onMounted, ref } from 'vue'
import Quiz from '@/components/Quiz.vue'

  const quiz = ref(null);
  const state = ref('loading')

  onMounted(() => {
    fetch('/settings.json')
      .then(r => {
        if(r.ok){
          return r.json()
        }
        throw new Error('Impossible de récupérer le json')
      })
      .then(data => {
        quiz.value = data
        state.value = 'idle'
      })
      .catch(e => {
        state.value = 'error'
      })
  })
</script>

<template>
  <div class="container">
    <p v-if="state === 'loading'">Chargement des données</p>
    <p v-if="state === 'error'">Une erreur s'est produite</p>

    <Quiz :quiz="quiz" v-if="quiz !== null" />
  </div>
</template>