<script setup lang="ts">
import Ruler from "../src/Ruler.vue";
// import HelloWorld from './components/HelloWorld.vue'
import HelloWorld from './HelloWorld.vue'

</script>

<template>
  <Ruler class="content" v-ruler:horizontal="10" v-ruler:vertical="10">
    <!-- Your content here -->
    <HelloWorld msg="Vite + Vue" />
  </Ruler>
</template>

<style scoped>
#app {

  padding-left: 30px;
  padding-top: 30px;
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
