<template>
  <div id="feest" class="container">
    <h3>donderdag 9 mei</h3>
    <h1 class="event-title">20:00</h1>
    <h1 class="event-title" style="margin-bottom: 0.5rem;">DANSFEEST</h1>
    <p class="subtitle">Met dessertenbuffet</p>
    <div class="section">
      <h1 class="section-title">LOCATIE</h1>
      <p class="subtitle">T’ile Malines</p>
    <a href="https://maps.app.goo.gl/2PmCDFNvhe57tZtWA">Rode-Kruisplein 12, 2800 Mechelen</a>
      <Location class="location" address="Grote Markt 9, 3000 Leuven" location="Stadhuis Leuven" src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2509.076059048124!2d4.465224276856577!3d51.03321594523281!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47c3e5bf16ff06e9%3A0x3a63047e4ef33a7d!2sRode-Kruisplein%2012%2C%202800%20Mechelen!5e0!3m2!1snl!2sbe!4v1709498464445!5m2!1snl!2sbe"></Location>
    </div>

    <div class="section">
      <h1 class="section-title">PARKING</h1>
     
        <p class="subtitle">Parking Indigo Mechelen Keerdok</p>
        <a href="https://maps.app.goo.gl/Mbfo7zjpkSSUHVqf6">Antonia Wolversstraat 1, 2800 Mechelen</a>
      </div>

      <div class="section">
      <h1 class="section-title">OVERNACHTING</h1>
        <p style=" font-weight: bold;">- Hotel Van der Valk -</p>
        <p>Krijg <span>10% </span>korting op kamers inclusief ontbijt door je reservatie te maken via <a href=mailto:info@hotel-mechelen.be>info@hotel-mechelen.be</a> met vermelding van:</p><p style="margin-left: 1rem; margin-top:1rem; font-weight:400">Trouw Nina en Gert - 9 mei 2024 - Code Malines</p>
        <p style="margin-top: 1rem;font-weight: bold;">- Hotel het Anker -</p>
        <p style="">Slechts 20 kamers dus wees er snel bij!</p><a style="margin-bottom: 1.5rem;" href="www.hetanker.be/nl/overnachten-in-de-brouwerij">Boek hier</a>
      </div>
  </div>
</template>
<script>
/* eslint-disable vue/multi-word-component-names */
import Location from './Location.vue';

export default {
  name: 'FeestInfo',
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
  flex-direction: column;
  width: 100%;
  height: 100%;
  justify-content: start;
  padding: 3rem 2rem 3rem 2rem;
  background-color: #BDCAAE;
  color: #68121B !important;
}

a {
  color: #68121B !important;
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
  .container {
    justify-content: start;
  }
  .section {
    width: 100%;

    h2 {
      width: 100%;
    }
  }
}
</style>
