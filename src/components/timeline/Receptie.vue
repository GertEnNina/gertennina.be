<template>
  <div id="receptie" class="container">
    <p class="subtitle">Woensdag 8 mei, 18:00</p>
    <h1>Walking dinner</h1>
    <h2>Abdij Keizersberg, Mechelsestraat 202, 3000 Leuven</h2>
    <div class="section">
      <h2>Route en parking</h2>
      <Location address="Mechelsestraat 202, 3000 Leuven" location="Abdij Keizersberg" src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2516.8997232988745!2d4.693666576430995!3d50.888566271679174!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47c160c31763da33%3A0x13b27b33cd030033!2sAbdij%20Keizersberg!5e0!3m2!1snl!2sbe!4v1709492069058!5m2!1snl!2sbe"></Location>
    </div>
    <div class="section">
      <h2>Menu</h2>
    </div>
  </div>
</template>
<script>
/* eslint-disable vue/multi-word-component-names */
import Location from './Location.vue';

export default {
  name: 'BurgerlijkeInfo',
  components: {
    Location
  },
  props: {},
  data() {
    return {

    }
  },
  watch: {

  },
  computed: {

  }
}
</script>

<style scoped>
h1 {
  text-align: start;
  font-weight: 900;
  font-size: 3rem;
}

h2 {
  text-align: start !important;
}


.container {
  box-sizing: border-box;
  height: 100vh;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  width: 100%;
  padding: 3rem 2rem 3rem 2rem;
  background-color:  #E8FFCB;
  color: #68121B !important;
}

.subtitle {
  text-align: start;
  font-size: 1rem;
}

.p {
  font-weight: bold;
}

.section {
  margin: 1.5rem 0 0 0;
  display: flex;
  flex-direction: column;
  width: 100%;

  h2 {
    width: 30%;
    text-align: start;
    border-bottom:  1px solid #68121B;
    margin-bottom: 1rem;
    font-weight: bold;
  }
}

@media only screen and (max-width: 600px) {
  .section {
    width: 100%;
  }
}
</style>
