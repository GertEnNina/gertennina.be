<template>
  <div class="background-container">
    <div class="hotel-info-container">
      <div class="hotel-info-content">
        <!-- <div class="title-column">
          <h1>Al een</h1>
        </div> -->
        <div class="info-column">
          <div>
            <h1>Overnachten in Mechelen?</h1>
            <p class="subtitle">Hier zijn enkele suggesties...</p>
          </div>
          <div class="hotel-info-elements-container">
            <div v-for="hotel in hotelInfo" :key="hotel.name" class="hotel-info-element">
              <h2 class="hotel-name">{{ hotel.name }}</h2>
              <p class="info-element">Op <span style="font-weight: 400;">{{ hotel.distance }} m </span> wandelen van T'ile Malines,  <span style="font-weight: 400;">{{ hotel.nRooms }}</span> beschikbare kamers</p>
              <div class="disclaimer" v-html="hotel.disclaimer"></div>
            </div>
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
          disclaimer: '<p>Krijg <span style="font-weight: 600">10 % </span> op kamers inclusief ontbijt door je reservatie te maken via <a href=mailto:info@hotel-mechelen.be>info@hotel-mechelen.be</a> met vermelding van:<p><p style="margin-left: 1rem; margin-top:1rem; font-weight:400">Trouw Gert en Nina</p><p style="margin-left: 1rem; margin-top: 1rem; font-weight: 400">9 mei 2024</p><p style="margin-left: 1rem; margin-top: 1rem; font-weight: 400">Code Malines</p>'
        },
        {
          name: 'Hotel het Anker',
          distance: 500,
          nRooms: 20,
          disclaimer: '<p class="urgent">Slechts 20 kamers dus wees er snel bij!<p><a href="www.hetanker.be/nl/overnachten-in-de-brouwerij"></a>'
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
  /* background-image: url('../assets/tiles_malines.jpg'); */
  background-repeat: no-repeat;
  background-size: cover;
}

.hotel-info-container {
  width: 90%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: end;
}

.hotel-info-content {
  display: flex;
  /* margin-right: 5rem; */
  place-self: end;
  width: 100%;
  height: 100%;
  /* border-radius: 0.5rem; */
  opacity: 100%;
}

.title-column {
  padding: 2rem 1rem 0 2rem;
  background-color: rgba(235, 235, 235, 0.4);
  width: 20%;
  backdrop-filter: blur(0.2rem);
}

.title-column h1 {
  text-align: end;
  color: #ebebeb;
}

.info-column {
  width: 100%;
  padding: 5rem;
  background-color: #ebebeb;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 2rem;
}

.hotel-info-elements-container {
  /* padding: 1rem; */
  display: flex;
  flex-direction: column;
  gap: 3rem;
  width: 100%;
}

.hotel-info-element {
  /* padding: 2rem; */
  /* border: solid 1px #39393A; */
  border-radius: 0.5rem;
  width: 100%;
  height: 100%;
}
.info-element {
  text-align: start;
  /* font-weight: 600; */
}

.disclaimer {
  text-align: start;
  margin: 0.5rem 0 0.5rem 0;
}

.hotel-name {
  font-size: 2rem;
  text-align: start;
  margin: 0.5rem 0 1rem 0;
  color: #39393A;
}

.subtitle {
  color: #39393A;
  text-align: start;
  font-size: 1rem;
}
</style>
