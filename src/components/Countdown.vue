<template>
  <div class="countdown-container">
    <h1 class="masked-string" :style="image">{{ timeString }}</h1>
  </div>
</template>

<script>
import moment from 'moment';
const weddingDate = '2024/05/09'

export default {
  name: 'CountdownComponent',
  props: {},
  data() {
    return {
      timeUntil: moment.duration(moment(weddingDate).diff(moment()))
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.countdown-container {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  /* text-align: start; */
}
.masked-string {
  font-weight: 900;
  margin-top: 0;
  margin-bottom: 0;
  font-size: 26rem;
  letter-spacing: -10px;
  line-height: 90%;
  text-transform: uppercase;
  font-family: 'Open Sans Pro', sans-serif;
  background-size: 80%;
  background-position: 50% 20%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
