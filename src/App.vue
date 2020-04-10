<template>
  <div id="app">
   <Kursinfo />
  </div>
</template>

<script>

import Kursinfo from './components/Kursinfo.vue';
export default {
  name: 'App',
  components: {
    Kursinfo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 60px;
}
</style>
