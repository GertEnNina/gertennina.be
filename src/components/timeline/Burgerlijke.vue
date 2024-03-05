<template>
  <div id="burgerlijke" class="container">
    <h3>woensdag 8 mei</h3>
    <h1 class="event-title">11:25</h1>
    <h1 class="event-title" style="margin-bottom: 0.5rem;">BURGERLIJK HUWELIJK</h1>
    

    <div class="section">
      <h1 class="section-title">LOCATIE</h1>
      <p class="subtitle">Stadhuis Leuven</p>
    <a href="https://maps.app.goo.gl/pLQpuQENVWaSpwsW9">Grote Markt 9, 3000 Leuven</a>
      <Location class="location" address="Grote Markt 9, 3000 Leuven" location="Stadhuis Leuven" src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2517.421659679618!2d4.69861247643042!3d50.878905771677175!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47c160d9b1d94719%3A0xf36ef92d64506731!2sHistorisch%20Stadhuis%20van%20Leuven!5e0!3m2!1snl!2sbe!4v1709490066760!5m2!1snl!2sbe"></Location>
    </div>

    <div class="section">
      <h1 class="section-title">PARKING</h1>
     
        <p class="subtitle">Q-Park Leuven Heilig Hart</p>
        <a href="https://maps.app.goo.gl/F4D1mxhdpFD3YgBV8">Naamsestraat 102, 3000 Leuven</a>
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
  font-size: 2rem;
  text-align: center;
}

h2 {
  
}

h3 {
  font-size: 2.5rem;
}

.event-title {
  font-size: 1.5rem;
}

.section-title {
  font-size: 1rem;
  margin-bottom: 0.5rem;
}
.container {
  box-sizing: border-box;
  overflow-y: auto;
  display: flex;
  justify-content: center;
  flex-direction: column;
  width: 100%;
  height: 100%;
  padding: 3rem 2rem 3rem 2rem;
  background-color: #8C3708;
  color: #F0EFE4 !important;
}

a {
  color: #F0EFE4 !important;
  font-weight: bold;
}

.subtitle {
  font-size: 1rem;
}

.section {
  margin: 1.5rem 0 0 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 50%;
  align-self: center;

  h2 {
    align-self: center;
    text-align: center;
    border-bottom:  1px solid #F0EFE4;
    font-weight: normal;
  }
  
}

.location {
  align-self: center;
}

@media only screen and (max-width: 600px) {
  .section {
    width: 100%;

    h2 {
      width: 100%;
    }
  }
}
</style>
