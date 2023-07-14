<template>
  <Countdown></Countdown>
</template>

<script>
import Countdown from './components/Countdown.vue';
export default {
  name: 'App',
  components: {
    Countdown
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #ebebeb;
  overflow: hidden;
  height: 100vh;
  width: 100vw;
}

body {
  margin: 0;
}
</style>
