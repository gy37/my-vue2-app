<template>
  <div id="app">
    <ComputedWatch />
    <VIf />
    <VFor />
    <VOn />
    <VModel />
    <button-counter></button-counter>
    <local-button-counter></local-button-counter>
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ComputedWatch from './components/ComputedWatch.vue'
import VIf from './components/VIf.vue';
import VFor from './components/VFor.vue';
import VOn from './components/VOn.vue';
import VModel from './components/VModel.vue';
import Vue from 'vue';
export default {
  name: 'App',
  components: {//局部组件
    HelloWorld,
    ComputedWatch,
    VIf,
    VFor,
    VOn,
    VModel,
    'local-button-counter': {
      data: function () {
        return {
          count: 0,
        }
      },
      template: '<button v-on:click="count++">You clicked me(local) {{ count }} times.</button>'
    }
  }
}

//全局组件
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0,
    }
  },
  template: '<button v-on:click="count++">You clicked me(global) {{ count }} times.</button>'
});

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

.logo:nth-last-child(2) {
  transform: translateX(-50px);
}

.logo:nth-last-child(3) {
  transform: rotate(180deg);
}

.logo:nth-last-child(4) {
  transform: translateX(50px);
}


label {
  margin-right: 8px;
}
</style>
