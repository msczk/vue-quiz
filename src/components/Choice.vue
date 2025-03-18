<script setup>
defineProps({
  id: String,
  value: String
})

const model = defineModel()
</script>

<template>
  <label :for="id">
    <input :id="id" name="answer" type="radio" :value="value" v-model="model">
    {{value}}
  </label>
</template>
