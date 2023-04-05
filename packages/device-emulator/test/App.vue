<script setup lang="ts">
import { ref } from 'vue'
import DeviceEmulator from "../src/DeviceEmulator.vue";
import HelloWorld from './components/HelloWorld.vue'
const disableScaling = ref(false)
const width = ref(335)
const height = ref(667)
</script>

<template>
  <DeviceEmulator class="device-emulator" :width="width" :height="height" :disable-scaling="disableScaling">
    <HelloWorld msg="Vite + Vue" />
  </DeviceEmulator>
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
  background-color: rgb(250, 235, 215, 0.3);
}
</style>
