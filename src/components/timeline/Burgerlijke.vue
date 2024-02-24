<template>
  <div class="background-container">
  </div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

export default {
  name: 'BurgerlijkeInfo',
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
  gap: 3rem;
}

.hotel-info-elements-container {
  /* padding: 1rem; */
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
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
