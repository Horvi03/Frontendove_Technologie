<script setup>
import { computed } from 'vue'

const props = defineProps({
  numberAsString: {
    type: String,
    required: true,
  },
})

// computed prepočíta počet číslic vždy, keď sa zmení hodnota od rodiča.
const digitCount = computed(() => {
  return props.numberAsString.length
})
</script>

<template>
  <section>
    <h2>Komponent B</h2>

    <p>Hodnota ako reťazec: „{{ numberAsString }}“</p>
    <p>Počet číslic: {{ digitCount }}</p>
  </section>
</template>