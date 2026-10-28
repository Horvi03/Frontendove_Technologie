<script setup>
const props = defineProps({
  title: String,
  text: String,
  author: Object,
})
</script>

<template>
  <h1>{{ props.title }}</h1>
  <br>
  <i>{{ props.author.firstName }} {{ props.author.lastName }}</i>
  <br>
  <p>{{ props.text }}</p>
</template>