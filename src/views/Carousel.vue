<template>
  <h1>Carousel</h1>
  <div>
    <v-carousel progress cycle>
      <v-carousel-item v-for="image in images"></v-carousel-item>
    </v-carousel>
  </div>
</template>
<script setup>
const props=defineProps(['images'])
</script>
<style>
  
</style>