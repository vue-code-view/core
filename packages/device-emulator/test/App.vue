<script setup lang="ts">
import { ref } from 'vue'
import DeviceEmulator from "../src/DeviceEmulator.vue";
// import HelloWorld from './components/HelloWorld.vue'
import HelloWorld from './components/MediaQueryToolbar.vue'
import Ruler from './components/Ruler.vue';
const disableScaling = ref(false)
const width = ref(335)
const height = ref(667)
</script>

<template>
  <Ruler class="content" v-ruler:horizontal="10" v-ruler:vertical="10">
    <!-- Your content here -->

    <DeviceEmulator class="device-emulator" :width="width" :height="height" :disable-scaling="disableScaling">
      <HelloWorld msg="Vite + Vue" />
    </DeviceEmulator>
  </Ruler>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.device-emulator {
  /* width: 80%;
  height: 40%; */
  background-color: rgb(250, 235, 215, 0.3);
}
</style>
