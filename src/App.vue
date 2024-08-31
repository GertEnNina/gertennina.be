<template>
  <component :is="currentView" />
</template>

<script>
import Register from './pages/Register.vue'
import ThankYou from './pages/ThankYou.vue';
import Timeline from './pages/Timeline.vue'

const routes = {
  '/': ThankYou,
}

export default {
  name: 'App',
  components: {
    Register,
    Timeline,
    ThankYou
  },
  data() {
    return {
      currentPath: window.location.pathname
    }
  },
  computed: {
    currentView() {
      console.log('view changed: ', this.currentPath);
      return routes[this.currentPath || '/'];
    }
  },
  mounted() {
    window.addEventListener('locationchange', () => {this.currentPath = window.location.pathname;})
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Barlow:wght@900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Barlow:wght@600&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Barlow:wght@300&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Google+Sans+Mono:wght@700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Google+Sans+Mono:wght@600&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Google+Sans+Mono:wght@500&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Google+Sans+Mono:wght@400&display=swap');

@font-face {
    font-family: 'Brittany';
    src: url('./assets/fonts/BrittanySignature.ttf');
}

h1, h2  {
  font-family: 'Barlow', sans-serif;
  margin: 0;
}

p, a {
  font-family: 'Google Sans Mono', sans-serif;
  margin: 0;
}

h3 {
  font-family: 'Brittany', sans-serif;
  margin: 0;
}

a {
  text-decoration: none;
  font-weight: normal !important;
  background-color: none;
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
