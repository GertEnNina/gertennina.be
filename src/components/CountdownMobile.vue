<template>
  <div class="countdown-container">
    <div class="countdown-elements-container" :style="image">
      <div class="amount-column">
        <h1 class="item">{{ (Math.floor(timeUntil.asDays())) }}</h1>
        <h2 class="unit">Dagen</h2>
        <h1 class="item">{{ (timeUntil.hours()).pad() }}</h1>
        <h2 class="item">Uren</h2>
        <h1 class="item">{{ (timeUntil.minutes()).pad() }}</h1>
        <h2 class="item">Minuten</h2>
        <h1 class="item">{{ (timeUntil.seconds()).pad() }}</h1>
        <h2 class="item">Seconden</h2>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

import moment from 'moment';
const weddingDate = '2024/05/09 13:30:00'

export default {
  name: 'CountdownMobile',
  props: {},
  data() {
    return {
      timeUntil: moment.duration(moment(weddingDate).diff(moment())),
    }
  },
  watch: {
    timeUntil: {
      handler(val) {
        if (val.seconds() >= 0) {
          setTimeout(() => {
            this.timeUntil = moment.duration(moment(weddingDate).diff(moment()))
          }, 1000);
        }
      },
      immediate: true,
      deep: true
    }
  },
  computed: {
    timeString() {
      return (Math.floor(this.timeUntil.asDays())) + " " + (this.timeUntil.hours()).pad() + ':' + (this.timeUntil.minutes()).pad() + ':' + (this.timeUntil.seconds()).pad();
    },
    image() {

      return {
        backgroundImage: `url(${require('../assets/test.jpg')})`
      }
    }
  }
}
</script>

<style scoped>
.countdown-container {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;

  /* text-align: start; */
}


h1 {
  font-weight: 900;
  margin-top: 0;
  margin-bottom: 0;
  padding: 0;
  font-size: 6rem;
  line-height: 90%;
}

h2 {
  padding: 0;
  font-weight: 900;
  margin-top: 0;
  margin-bottom: 0;
  font-size: 4rem;
  line-height: 90%;
}

.countdown-elements-container {
  display: flex;
  /* gap: 2rem; */
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-transform: uppercase;
  background-size: 80%;
  background-position: 50% 20%;
  padding: 1rem 0 1rem 0;
  /* margin: 1rem 0 1rem 0; */
}

.amount-column {
  flex-grow: 1;
  justify-content: center;
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  text-align: center;
}

.unit-column {
  flex-grow: 1;
  justify-content: start;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  text-align: start;
}

.item-container {
  height: 100%;
  display: flex;
  flex-direction: column;
  vertical-align: bottom;
}

.item {
  height: 5rem;
}
</style>
