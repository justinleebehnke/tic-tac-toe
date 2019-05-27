<template>
  <div id="app">
    <MiniGame></MiniGame>
  </div>
</template>

<script>
import MiniGame from './components/MiniGame'
export default {
  name: 'app',
  components: {
    MiniGame
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
