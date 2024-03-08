<template>
  <div id="faq" class="container">
    <h1 class="event-title" style="margin-bottom: 0.5rem;">Extra informatie</h1>
    <div class="section">
      <h1 class="section-title">Wat kunnen we jullie cadeau geven?</h1>
      <p class="subtitle">We zijn ontzettend dankbaar om samen met jullie dit belangrijk moment te kunnen beleven. We hebben al meer potten, pannen en servies dan we nodig hebben, maar we zouden enorm blij zijn met een bijdrage aan onze huwelijksreis. Als je graag iets wilt schenken, kan dat via ons rekeningnummer BE76 7441 0004 6395.</p>
    </div>
    
    <div class="section">
      <h1 class="section-title">Wil je ons graag verassen tijdens ons feest?</h1>
      <p class="subtitle">Super fijn, alvast bedankt. Neem contact op met onze ceremoniemeester, Lennart Steenberghs, via <span style="font-weight: bold;">lennart.steenberghs@gmail.com</span>. Zo kunnen we er voor zorgen dat alles soepel verloopt en wij zeker voldoende aandacht hebben voor jou.</p>
    </div>

    <div class="section">
      <h1 class="section-title">Wat moet ik aandoen?</h1>
      <p class="subtitle">Het belangrijkste is dat je iets draagt waarin je je goed voel. Als je toch zou twijfelen, ga dan voor casual chic.</p>
    </div>

    <div class="section">
      <h1 class="section-title">Mogen we foto's nemen tijdens de ceremonie en het feest?</h1>
      <p class="subtitle">Natuurlijk! <span style="font-weight: bold;">Tijdens de ceremonie willen we echter een intieme sfeer behouden, dus vragen we om geen foto's te maken tijdens dit deel van de dag</span>. Onze fotograaf zal zorgen voor prachtige beelden die we graag met jullie wullen delen na afloop van het feest.</p>
    </div>

    <div class="section">
      <h1 class="section-title">Wie heeft die mooie foto's van jullie getrokken?</h1>
      <p class="subtitle">De foto op de welkomstpagina van deze website is getrokken door Martijn Margullier. De foto op de uitnodiging is getrokken door Kaat Van der Brempt.</p>
    </div>
    
    <div class="section">
      <h1 class="section-title">Ik heb een vraag waarop ik nog geen antwoord heb gevonden. Hoe kan ik jullie contacteren?</h1>
      <p class="subtitle" style="margin-bottom: 1.5rem;">Als je nog een vraag hebt, kan je ons bereiken door een mailtje te sturen naar <span style="font-weight: bold;">gert.nina.vdbstb@gmail.com</span>. Liever via de post? Ons adres is Jean-Baptiste Van Monsstraat 77 bus 0002, 3000 Leuven.</p>
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
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  width: 100%;
  text-align: start;
}
.container {
  box-sizing: border-box;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  padding: 3rem 2rem 3rem 2rem;
  justify-content: start;
  background-color: #ebebeb;
  color: #39393A !important;
}

a {
  color: #39393A !important;
  font-weight: bold;
}

.subtitle {
  font-size: 1rem;
  text-align: start;
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
