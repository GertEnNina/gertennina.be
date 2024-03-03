<template>
  <div class="location-container">
    <div class="maps-container">
      <iframe class="maps-frame" :src="src" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
    </div>
    <div class="info-container">

    </div>
  </div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

export default {
  name: 'Location',
  props: {src: String, location: String, address: String},
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
.location-container {
  box-sizing: border-box;
  display: flex;
  gap: 2rem;
  height: 400px;
  width: 70%;
  padding: 0.5rem 0.5rem 0.5rem 0.5rem;
}

.info-container {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  text-align: start;
  height: 100%;
  width: 30%;
}

.maps-container {
  flex: 1 1 auto;
  overflow: hidden;
  box-sizing: border-box;
  display: flex;
  height: 100%;
  width: 70%;
}

.maps-frame {
  width: 100%;
  height: 100%;
}

@media only screen and (max-width: 600px) {
  .location-container {
    flex-direction: column;
    width: 100%;
  }
  .info-container {
    height: 40%;
    width: 100%;
    text-align: start;
  }

  .maps-container {
    height: 60%;
    width: 100%;
  }
}


</style>
