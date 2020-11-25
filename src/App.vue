<template>
  <div id="app">
    <!-- <Shuttle /> -->
    <Tshuttle />
  </div>
</template>

<script>
// import Shuttle from './components/HelloWorld.vue'
import Tshuttle from './components/TableShuttle.vue'

export default {
  name: 'App',
  components: {
    // Shuttle,
    Tshuttle,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
