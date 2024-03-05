<template>
  <div id="faq" class="container">
    <h1 class="event-title" style="margin-bottom: 0.5rem;">FAQ</h1>
    
    <div class="section">
      <h1 class="section-title">Wil je ons graag verassen tijdens ons feest?</h1>
      <p class="subtitle">Super fijn, alvast bedankt. <span style="font-weight: bold;">Lennart Steenberghs</span> is onze ceremoniemeester van dienst, laat hem dus zeker iets weten via ... of op de dag zelf zodat alles soepel verloopt en wij zeker genoeg aandacht hebben voor jou.</p>
    </div>

    <div class="section">
      <h1 class="section-title">Wat moet ik aandoen?</h1>
      <p class="subtitle">Voor ons is het vooral belangrijk dat je aandoet waar je je goed bij voelt, maar moest je toch nog twijfelen, ga dan voor <span style="font-weight: bold;">casual chique</span> .</p>
    </div>

    <div class="section">
      <h1 class="section-title">Mogen we foto's trekken?</h1>
      <p class="subtitle" style="margin-bottom: 1.5rem;">Natuurlijk! We zouden het geweldig vinden als jullie deel uitmaken van het vastleggen van onze speciale dag. <span style="font-weight: bold;">Tijdens de ceremonie en het belangrijkste deel van het feest vragen we echter om geen foto's te maken</span>, zodat iedereen volledig kan genieten en aanwezig kan zijn. Onze fotograaf neemt het vastleggen van deze momenten voor zich en we zullen er voor zorgen dat alle foto's toegankelijk gemaakt worden voor jullie!</p>
    </div>
  </div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

export default {
  name: 'FAQInfo',
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
  padding: 3rem 2rem 3rem 2rem;
  justify-content: center;
  background-color: #ebebeb;
  color: #39393A !important;
}

a {
  color: #39393A !important;
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
