<script setup>
import { computed, ref, watch } from 'vue'
import { shuffleArray } from '@/functions/array.js'
import Choice from '@/components/Choice.vue'

const props = defineProps({
  question: Object
})
const answer = ref(null)
const emits = defineEmits(['answer'])

const randomChoices = computed(() => shuffleArray(props.question.choices))
</script>

<template>
  <article>
    <h3>{{question.question}}</h3>
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice">
        <Choice :id="`answer-${index}`" :value="choice" v-model="answer" />
      </li>
    </ul>
    <p v-if="answer">Votre réponse : {{answer}}</p>
    <button :disabled="answer === null" @click="emits('answer', answer)">Suivant</button>
  </article>
</template>