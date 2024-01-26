<template>
  <div :class="{'fullScreen':fullScreen}">
    <v-carousel :class="{ 'carousel': fullScreen }" progress cycle >
      <v-carousel-item class="carousel-item" v-for="base in base64">
        <img :src="base" alt="">
      </v-carousel-item>
    </v-carousel>
      <v-btn class="fullScreenButton" @click="handleFullScreen" >FullScreen</v-btn>
  </div> 
  <br>
</template>
<script setup>
import { onMounted, ref } from 'vue'
const props = defineProps(['base64']);
const emits=defineEmits(['fullScreen'])
const fullScreen = ref(false)
function handleFullScreen() {
  fullScreen.value = !fullScreen.value
  emits('fullScreen');
}
</script>
<style scoped>
.carousel{
  height: 95vh!important;
}

.fullScreenButton{
  position: absolute;
  bottom: 5%;
  right: 5%;
}
.fullScreen{
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  top:2%;
  left: 2%;
  width: 95vw;
  height: 95vh;

}
.carousel-item{
}
img{
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>