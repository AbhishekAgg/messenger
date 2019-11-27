<template>
  <div id="app">
    <Messenger />
  </div>
</template>

<script>
import Messenger from './pages/messenger/index.vue'

export default {
  name: 'app',
  components: {
    Messenger,
  },
};
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
</style>
