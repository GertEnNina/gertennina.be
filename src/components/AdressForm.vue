<template>
  <div class="background-container">
    <div class="adress-form-container">
      <div class="adress-form-content">
        <!-- <div class="title-column">
          <h1>Al een</h1>
        </div> -->
        <div class="info-column">
          <div>
            <h1>Naar welk adres mogen we de uitnodiging sturen?</h1>
            <!-- <p class="subtitle">Hier zijn enkele suggesties...</p> -->
          </div>
          <div id="hubspotForm" v-once></div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

export default {
  name: 'AdressForm',
  props: {},
  data() {
    return {
    }
  },
  watch: {

  },
  computed: {

  },
  mounted() {
    const script = document.createElement("script");
    script.src = "https://js-eu1.hsforms.net/forms/v2.js";
    document.body.appendChild(script);
    script.addEventListener("load", () => {
      if (window.hbspt) {
        window.hbspt.forms.create({
          region: "eu1",
          portalId: "140826681",
          formId: "7edff67a-3a56-4dbc-9f04-c8f5b6963ab5",
          target: "#hubspotForm"
        })

      }
    })
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

.adress-form-container {
  width: 90%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: end;
}

.adress-form-content {
  display: flex;
  /* margin-right: 5rem; */
  place-self: end;
  width: 100%;
  height: 100%;
  /* border-radius: 0.5rem; */
  opacity: 100%;
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
</style>
