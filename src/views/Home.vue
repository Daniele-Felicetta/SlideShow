<template>
  <div  class="my-root">
    <div :class="{ 'hide': fullScreen }" v-if="!start">
      <v-card class="cardInput pa-10 d-flex flex-column">
        <v-card-title>Inserisci i file</v-card-title>
        <v-card-subtitle>Assicurati che i tuoi file siano solo immagini</v-card-subtitle>
        <v-file-input class="input pt-8" ref="imageInput" @change="(e) => handleSelected(e)" multiple prepend-icon="mdi-image"
          v-model="images"></v-file-input>
        <v-btn class="align-self-md-end"
          @click="() => start = true">Go<v-icon>mdi-arrow-right-drop-circle</v-icon></v-btn>
      </v-card>
    </div>

    <div :class="{ 'z-idx': fullScreen }" class="carousel" v-else>
      <v-btn class="close" icon="mdi-exit-run" @click="() => start = false"></v-btn>
      <Carousel @fullScreen="handleFullScreen" :base64="base64" :start="start" :imageInput="imageInput" :images=images></Carousel>
    </div>

    <div :class="{ 'hide': fullScreen }">
      <v-btn  class="showFrameButton d-none d-lg-flex" icon="mdi-fullscreen-exit"
      @click="() => showFrame = !showFrame"></v-btn>
      <div class="d-flex flex-column ml-8" :class="{ 'hide': !showFrame }">
        <iframe class="d-none d-lg-flex framePage" :class="{ framePageMinus: resizeFrame }"
        src="https://vuetifyjs.com/en/getting-started/installation/#installation" frameborder="20"></iframe>
        <v-btn @click="() => resizeFrame = !resizeFrame">{{ resizeFrame ? "Reduce" :  "Larger" }}</v-btn>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Carousel from './Carousel.vue';
const start = ref(false);
const images = ref([]);
const showFrame = ref(false);
const resizeFrame = ref(false);
const imageInput = ref(null);
const base64 = ref([]);
const fullScreen = ref(false);

function handleFullScreen(){
  fullScreen.value = true;
}

function handleSelected(e) {
  console.log('ciao')
  for (let i = 0; i < imageInput.value.files.length; i++) {
    const reader = new FileReader();
    const selectedFile = imageInput.value.files[i];
    if (selectedFile) {
      reader.onloadend = (evt) => {
        base64.value[i] = reader.result;
        console.log(base64.value[i]);
      }
      reader.readAsDataURL(selectedFile);
    }
  }
}
</script>

<style scoped>
.cardInput{
  max-width: 600px;
  width: 500px;
}
@media screen and (max-width: 500px){
  .cardInput{
    max-width: 300px;
    width: 250px;
  }
}
.input{
  word-break: break-all;
  
}
.my-root {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel {
  width: 60vw;
  display: block !important;
}

.close {
  position: absolute;
  top: 2rem;
  right: 5rem;
}

.hide {
  display: none !important;
}

.showFrameButton {
  position: absolute;
  top: 2rem;
  left: 5rem;
}

.framePage {
width: 40vw;
  height: 800px;
}

.framePageMinus {
  width: 60vw;
  height: 800px;

}
</style>
<style>
.z-idx{
  z-index: 999;
}
button{
  z-index: inherit;
}
</style>