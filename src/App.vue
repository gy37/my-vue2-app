<template>
  <div id="app">
    <ComputedWatch />
    <VIf />
    <VFor />
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ComputedWatch from './components/ComputedWatch.vue'
import VIf from './components/VIf.vue';
import VFor from './components/VFor.vue';
export default {
  name: 'App',
  components: {
    HelloWorld,
    ComputedWatch,
    VIf,
    VFor,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
}

.logo {
  width: 100px;
}

label {
  margin-right: 8px;
}
</style>
