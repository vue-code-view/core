<script setup lang="ts">
import { ref } from 'vue'
// import DeviceEmulator from "../src/DeviceEmulator.vue";
// import HelloWorld from './components/HelloWorld.vue'
// import HelloWorld from './components/MediaQueryToolbar.vue'
// import Ruler from './components/Ruler.vue';
import ViewporResizer from './components/ViewporResizer.vue'
import HelloWorld from './components/HelloWorld.vue'
// import ResizableContainer from './components/ResizableContainer.vue';
// const disableScaling = ref(false)
const width = ref(400)
const height = ref(300)
</script>

<template>
  <!-- <Ruler class="content" v-ruler:horizontal="10" v-ruler:vertical="10">
      <DeviceEmulator class="device-emulator" :width="width" :height="height" :disable-scaling="disableScaling">
        <HelloWorld msg="Vite + Vue" />
      </DeviceEmulator>
    </Ruler> -->
  <!-- <viewport-zoom></viewport-zoom> -->
  <ViewporResizer :width="width" :height="height">
    <!-- 在此处放入需要进行拖动缩放的内容 -->
    <template #content>
      <div>
        <a href="https://vitejs.dev" target="_blank">
          <img src="/vite.svg" class="logo" alt="Vite logo" />
        </a>
        <a href="https://vuejs.org/" target="_blank">
          <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
        </a>
      </div>
      <HelloWorld msg="Vite + Vue" />
    </template>
  </ViewporResizer>
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
