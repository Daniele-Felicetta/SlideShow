<template>
  <div class="my-root ">
    <div v-if="!start">
      <v-card class="pa-10 d-flex flex-column">
        <v-card-title>Inserisci i file</v-card-title>
        <v-card-subtitle>Assicurati che i tuoi file siano solo immagini</v-card-subtitle>
        <v-file-input class="pt-8" multiple prepend-icon="mdi-image" v-model="images"></v-file-input>
        <v-btn class="align-self-md-end" @click="() => start = true">Go <v-icon>mdi-arrow-right-drop-circle</v-icon>
        </v-btn>
      </v-card>
    </div>

    <div class="carousel" v-else>
      <v-btn class="close" icon="mdi-exit-run" @click="() => start= false"></v-btn>
      <Carousel images=images></Carousel>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Carousel from './Carousel.vue';
const start = ref(false)
const images = ref([])

</script>

<style scoped>
.my-root {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel {
  
}

.close {
  position: absolute;
  top:2rem;
  right: 5rem;
}
</style>