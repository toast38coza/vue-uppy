<template>
  <div id="app">
    <img src="./assets/logo.png">
    <uppy></uppy>
  </div>
</template>

<script>
import Uppy from './components/Uppy'

export default {
  name: 'app',
  components: {
    Uppy
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
