<template>
    <div>
      <v-btn
        stacked
        prepend-icon="mdi-thumb-down"
        @click="rate(0)"
        >Gefällt mir nicht</v-btn>
      <v-btn
        stacked
        prepend-icon="mdi-thumb-up"
        @click="rate(1)"
        >Gefällt mir</v-btn>
    </div>
    
  </template>
  
  <script>
  export default {
    methods: {
    rate(rating) {
      this.$emit('rated', rating)
        }
      }
    }
  </script>
  
  <style scoped>
  div {
    display: flex;
    align-items: center;
  }
  </style>