<template>
  <div id="app">
    <DryEraseBoard />
  </div>
</template>

<script>
import DryEraseBoard from './components/DryEraseBoard.vue'

export default {
  name: 'app',
  components: {
    DryEraseBoard
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
