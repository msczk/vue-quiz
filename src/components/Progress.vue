<script setup>
    defineProps({
      step: Number,
      total: Number
    })
</script>

<template>
  <div>
    Etape {{step}} / {{total}}
    <progress :value="step" :max="total"></progress>
  </div>
</template>