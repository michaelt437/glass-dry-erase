<template>
  <div id="app" class="container grid-sm">
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
body {
  background-color: #f9f9f9;
  background-color: #222532;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  color: #FFF;
  margin-top: 60px;
}
.card {
  transition: all .25s ease-out;
  background: transparent;
  border-color: transparent;
  border-left-color: #de0d65;
  border-left-width: .1rem;
  margin-top: 2rem;
  margin-bottom: 2rem;

  &:hover {
    background: #FFF;
    // border-color: #dadee4;
  }
}

.post {
  margin: 2rem 0 4rem;
  hr {
    border: none;
    border-top: 3px solid #de0d65;
    width: 5%;
    margin: 0 0 1rem;
  }
  &__footer {
    display: flex;
  }
}

.flex-spacer {
  flex-grow: 1;
}

.chip {
  margin-left: 0;
  margin-right: .2rem;
  border-radius: 0;
}
</style>
