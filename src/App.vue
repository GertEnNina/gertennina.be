<template>
  <VerticalCarousel :components="components">

  </VerticalCarousel>
</template>

<script>
import VerticalCarousel from './components/VerticalCarousel.vue'

export default {
  name: 'App',
  components: {
    VerticalCarousel
  },
  data() {
    return {
      carouselComponents: [
        'Countdown',
        'HotelInfo',
        'AdressForm',
      ]
    }
  },
  computed: {
    isMobile() {
      if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
        return true
      } else {
        return false
      }
    },
    components() {
      return this.carouselComponents.map((element) => {
        console.log(element);
        return element + (this.isMobile ? 'Mobile' : '');
      })
    }
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

h1,
h2 {
  font-family: 'Barlow', sans-serif;
  margin: 0;
}

p {
  font-family: 'Google Sans Mono', sans-serif;
  margin: 0;
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
