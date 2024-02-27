<template>
  <div style="background: beige">
    <h1>from component{{ count }}</h1>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const count = ref(0)

const increment = () => {
  count.value++
}

const double = () => {
  count.value *= 2
}

defineExpose({
  increment,
  count
})
</script>
