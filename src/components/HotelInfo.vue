<template>
  <div class="background-container">
    <div class="hotel-info-container">
      <div class="hotel-info-content">
        <div class="title-column">
          <h1>Al een</h1>
        </div>
        <div class="info-column">
          <div>
            <h1>hotel boeken?</h1>
            <h2 class="subtitle">Hier zijn enkele suggesties...</h2>
          </div>

          <div v-for="hotel in hotelInfo" :key="hotel.name" class="hotel-info-element">
            <h2 class="hotel-name">{{ hotel.name }}</h2>
            <p class="info-element">Op <span style="font-weight: 900;">{{ hotel.distance }}m </span> wandelen van de
              feestlocatie</p>
            <p class="info-element"><span style="font-weight: 900;">{{ hotel.nRooms }}</span> beschikbare kamers</p>
            <div class="disclaimer" v-html="hotel.disclaimer"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

export default {
  name: 'HotelInfo',
  props: {},
  data() {
    return {
      hotelInfo: [
        {
          name: 'Hotel Van der Valk',
          distance: 250,
          nRooms: 200,
          discountCode: 'Malines',
          disclaimer: '<p>Mail naar <span style="font-weight: 600"><a href=mailto:info@hotel-mechelen.be>info@hotel-mechelen.be</a></span> met vermelding van onderstaande:<p><p style="margin-left: 1rem; margin-top:1rem; font-weight: 600">Naam trouwkoppel</p><p style="margin-left: 1rem; margin-top: 1rem; font-weight: 600">Datum trouw</p><p style="margin-left: 1rem; margin-top: 1rem; font-weight: 600">Vermelding van de kortingscode: Malines</p>'
        },
        {
          name: 'Hotel het Anker',
          distance: 500,
          nRooms: 20,
          disclaimer: '<p class="urgent">Wees er snel bij!<p>'
        }
      ]
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

.background-container {
  height: 100%;
  width: 100%;
  background-image: url('../assets/tiles_malines.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}

.hotel-info-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: end;
}

.hotel-info-content {
  display: flex;
  margin-right: 5rem;
  place-self: end;
  width: 50%;
  height: 100%;
  /* border-radius: 0.5rem; */
  opacity: 100%;
}

.title-column {
  padding: 2rem 1rem 0 2rem;
  background-color: rgba(235, 235, 235, 0.4);
  width: 30%;
  backdrop-filter: blur(0.2rem);
}

.title-column h1 {
  text-align: end;
  color: #ebebeb;
}

.info-column {
  width: 70%;
  padding: 2rem 0rem 0 1rem;
  background-color: #ebebeb;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.info-element {
  text-align: start;
  font-weight: 600;
}

.disclaimer {
  text-align: start;
  margin: 0.5rem 0 0.5rem 0;
}

.hotel-name {
  font-size: 2rem;
  text-align: start;
  margin-top: 0.5rem;
  color: #39393A;
}

.subtitle {
  color: #39393A;
  text-align: start;
  font-size: 1rem;
}

</style>
