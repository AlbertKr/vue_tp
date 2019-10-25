<template>
  <div id="app">
    <Board />
  </div>
</template>

<script>
import Board from './components/Board.vue'
export default {
  name: 'app',
  components: {
    Board
  },
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
  min-width: 100%;
  max-width: 100%;
  min-width: 100%;
  max-width: 100%;
}
</style>