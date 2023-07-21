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
/* @import url('https://fonts.googleapis.com/css2?family=Jost:wght@900&display=swap');

h1,
h2,
p {
  font-family: 'Jost', sans-serif;
} */

@import url('https://fonts.googleapis.com/css2?family=Barlow:wght@900&display=swap');

h1,
h2,
p {
  font-family: 'Barlow', sans-serif;
}

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
