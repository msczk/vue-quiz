<script setup>
import { computed } from 'vue'

const props = defineProps({
  id: String,
  value: String,
  disabled: Boolean,
  answer: String
})

const model = defineModel()

const classes = computed(() => ({
  right: props.disabled && props.value === props.answer,
  wrong: props.disabled && props.value !== props.answer,
}))
</script>

<template>
  <label :class="classes" :for="id">
    <input  :disabled="disabled" :id="id" name="answer" type="radio" :value="value" v-model="model">
    {{value}}
  </label>
</template>

<style scoped>
  .right{
    color: green;
  }

  .wrong{
    color: red;
  }
</style>