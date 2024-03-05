<template>
  <div class="container">
    <h1 class="event-title" style="margin-bottom: 0.5rem;">Bevestig aanwezigheid</h1>
    
    <div class="section">
      <HubspotForm :formType="guest.formType" :name="guest.name"></HubspotForm>
    </div>

  </div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */
import HubspotForm from './HubspotForm.vue';

export default {
    name: 'FormPage',
    props: { guest: Object },
    data() {
        return {};
    },
    watch: {},
    computed: {},
    components: { HubspotForm }
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
