<script setup>
    import Article from './Article.vue'
    class Person { constructor(firstName, lastName) {
    this.firstName = firstName
    this.lastName = lastName
}} 

const author = new Person('Jana', 'Nováková')
</script>

<template>
    <Article title="Clanok 1" text="Toto je text prvého článku" :author="author"/>
</template>