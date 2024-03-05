<template>
    <div v-if="guest === undefined" class="name-input-container">
      <div class="image-container">
      </div>
      <div class="name-input-form">
        <p>Wie mogen we ontvangen?</p>
        <input class="name-input" type="text" placeholder="Voornaam" v-model="firstName"/>
        <input class="name-input" type="text" placeholder="Achternaam" v-model="lastName"/>
        <button class="button" @click="setName()">Go</button>
      </div>
    </div>
    <div v-else class="timeline-container">
      <div v-if="currentScrollId > 0" class="arrow-up-container">
        <div class="arrow" @click="scrollUp()">
          <font-awesome-icon icon="fa-solid fa-arrow-up" class="icon" />
        </div>
      </div>
      <div class="welcome" id="welcome">
        <h2>Welkom {{ guest.name.split(" ")[0] }},</h2>
        <p style="margin-top: 0.5rem;">We ontvangen jou <span v-if="partner">en {{ partner.name.split(" ")[0] }}</span> graag om samen ons huwelijk te vieren.</p>
        <p style="margin-top: 1rem;">Gebruik de pijltjes boven - en onderaan de pagina om een kijkje te nemen naar het programma,</p>
        <p>het antwoord te vinden op veelgestelde vragen</p>
        <p>  <span style="font-weight: bold;">en vergeet aan het einde niet jou <span v-if="partner">en jouw partner zijn/haar</span> aanwezigheid te bevestigen</span>!</p>
        <div class="index">
          <p>Wil je snel iets terugvinden?</p>
          <p class="index-item" @click="scrollTo(1)">Programma</p>
          <p class="index-item" @click="scrollTo(6)" v-if="guest.formType !== 'receptie'">FAQ</p>
          <p class="index-item" @click="scrollTo(7)">Bevestig aanwezigheden</p>
        </div>
      </div>
      <div class="event-container">
        <component v-for="event in guest.events" :key="event" :is="event"></component>
        <div id="form" class="container">
          <Form :guest="guest"></Form>
        </div>
        <div v-if="partner" id="form_partner" class="container">
          <Form :guest="partner"></Form>
        </div>
      </div>
      <div v-if="currentScrollId !== scrollIds.length - (partner ? 1 : 2)" class="arrow-down-container">
          <div class="arrow" @click="scrollDown()">
            <font-awesome-icon icon="fa-solid fa-arrow-down" class="icon" />
          </div>
        </div>
    </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import Burgerlijke from '../components/timeline/Burgerlijke.vue';
import Receptie from '../components/timeline/Receptie.vue';
import Ceremonie from '../components/timeline/Ceremonie.vue';
import Diner from '../components/timeline/Diner.vue';
import Feest from '../components/timeline/Feest.vue';
import FAQ from '../components/timeline/FAQ.vue';
import Form from '../components/timeline/FormPage.vue';


const burgerlijkeComponent = Burgerlijke;
const receptieComponent = Receptie;
const ceremonieComponent = Ceremonie;
const dinerComponent = Diner;
const feestComponent = Feest;
const faqComponent = FAQ;

const eventGroups = {
  all: [
      burgerlijkeComponent,
      receptieComponent,
      ceremonieComponent,
      dinerComponent,
      feestComponent,
      faqComponent
  ],
  full: [
      ceremonieComponent,
      dinerComponent,
      feestComponent,
      faqComponent
  ],
  partial: [
      ceremonieComponent,
      feestComponent,
      faqComponent
  ],
  receptie: [
      burgerlijkeComponent,
      receptieComponent
  ]
}

const guests = [
    // All
    {
        "name": "Gert Van der Brempt",
        "partner": "Nina Steenberghs",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Nina Steenberghs",
        "partner": "Gert Van der Brempt",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Bram Cousaert",
        "partner": "Lieze Van Dyck",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Lieze Van Dyck",
        "partner": "Bram Cousaert",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Merel De Maeseneer",
        "partner": "Sandra Lejeune",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Sandra Lejeune",
        "partner": "Merel De Maeseneer",
        "formType": "all",
        "events": eventGroups.all
    },

    // Full
    {
        "name": "Milos Korac",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Martijn Margullier",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Ruben Appeltans",
        "partner": "Liesbeth Vanlinthout",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Liesbeth Vanlinthout",
        "partner": "Ruben Appeltans",
        "formType": "full",
        "events": eventGroups.full
    },

    // Partial
    {
        "name": "Leander Pellaerts",
        "partner": "Jessica Reynders",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Jessica Reynders",
        "partner": "Leander Pellaerts",
        "formType": "partial",
        "events": eventGroups.partial
    },

    // Receptie
    {
        "name": "Roel Bervoets",
        "partner": "Lien Lefevre",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Lien Lefevre",
        "partner": "Roel Bervoets",
        "formType": "receptie",
        "events": eventGroups.receptie
    },

  ]

export default {
  name: 'TimelinePage',
  components: {
    FAQ,
    Form
  },
  data() {
    return {
      partner: undefined,
      firstName: undefined,
      lastName: undefined,
      guest: undefined,
      scrollIds: [
        "welcome",  
        "burgerlijke",
        "receptie",
        "ceremonie",
        "diner",
        "feest",
        "faq",
        'form',
        'form_partner'
      ],
      currentScrollId: 0
    }
  },
  methods: {
    setName() {
      this.getGuest(this.firstName + ' ' + this.lastName);
      window.location.hash = this.scrollIds[this.currentScrollId];
    },
    getGuest(name) {
      this.guest = guests.find((el) => {
        return el.name === name;
      });
      this.partner = guests.find((el) => {
        return el.name === this.guest.partner;
      });
    },
    scrollDown() {
      this.currentScrollId = (this.currentScrollId + 1) % this.scrollIds.length;
      const element = document.querySelector("#" + this.scrollIds[this.currentScrollId]);
      if (element) {
        document.querySelector("#" + this.scrollIds[this.currentScrollId]).scrollIntoView({
              behavior: 'smooth'
          });
          window.setTimeout(() => {
            window.location.hash = this.scrollIds[this.currentScrollId];
          }, 500);
      } else {
        this.scrollDown();
      }
    },
    scrollUp() {
      this.currentScrollId = (this.currentScrollId - 1) % this.scrollIds.length;
      const element = document.querySelector("#" + this.scrollIds[this.currentScrollId]);
      if (element) {
        document.querySelector("#" + this.scrollIds[this.currentScrollId]).scrollIntoView({
              behavior: 'smooth'
          });
      } else {
        this.scrollUp();
      }
    },
    scrollTo(index) {
      this.currentScrollId = index;
      const element = document.querySelector("#" + this.scrollIds[this.currentScrollId]);
      if (element) {
        document.querySelector("#" + this.scrollIds[this.currentScrollId]).scrollIntoView({
              behavior: 'smooth'
          });
      } else {
        this.scrollDown();
      }
    }
  },
  mounted() {

  },
  computed: {
    isMobile() {
      if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
        return true
      } else {
        return false
      }
    },
    components() {
      return this.timelineComponents.map((element) => {
        return element + (this.isMobile ? 'Mobile' : '');
      })
    },
  }
}
</script>

<style>

.name-input-container {
  padding: 2rem;
  height: 90vh;
  display: flex;
  justify-content: center;
  background-color: #ebebeb;
  color: #39393A !important;
}

.timeline-container {
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  position: relative;
  overflow-y: hidden;
  overflow-x: hidden
}

.index {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.index-item {
  font-weight: bold;
  cursor: pointer;
}

.event-container {
  height: 100vh;
  overflow-y: hidden;
  overflow-x: hidden
}

.image-container {
  background-image: url('../assets/image.png');
  position: absolute;
}

.name-input-form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  place-self: center;
  width: 400px;
}

.welcome {
  padding: 2rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-color: #ebebeb;
  color: #39393A !important;
}

.button {
    font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
    margin: 0;
    cursor: pointer;
    display: inline-block;
    font-weight: 700;
    line-height: 12px;
    position: relative;
    text-align: center;
    transition: all .15s linear;
    background-color: #ff7a59;
    border-color: #ff7a59;
    color: #fff;
    border-radius: 3px;
    border-style: solid;
    border-width: 1px;
    font-size: 14px;
    padding: 12px 24px;
}

.name-input {
    display: inline-block;
    width: 100%;
    max-width: 500px;
    height: 40px;
    padding: 9px 10px;
    font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
    font-size: 16px;
    font-weight: normal;
    line-height: 22px;
    color: #33475b;
    border: 1px solid #cbd6e2;
    box-sizing: border-box;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -ms-border-radius: 3px;
    border-radius: 3px;
}

.name-input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
}


.arrow {
  /* padding: 10px; */
  display: flex;
  justify-content: center;
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 9999px;
  height: 2.5rem;
  width: 2.5rem;
  cursor: pointer;
}

.icon {
  font-size: 1.5rem;
  place-self: center;
}

.arrow-down-container {
  z-index: 10;
  position: fixed;
  width: 100%;
  height: 3rem;
  display: flex;
  justify-content: center;
  bottom: 0;
  animation: MoveUpDown 2s linear infinite;
}

.arrow-up-container {
  z-index: 10;
  position: fixed;
  width: 100%;
  height: 3rem;
  display: flex;
  justify-content: center;
  top: 0;
  animation: MoveDownUp 2s linear infinite;
}

.container {
  box-sizing: border-box;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  justify-content: center;
  padding: 3rem 2rem 3rem 2rem;
  background-color: #ebebeb;
  color: #39393A !important;
}

@media only screen and (max-width: 600px) {
  .container {
    justify-content: start;
  }
}

@keyframes MoveUpDown {

  0%,
  100% {
    bottom: 0;
  }

  50% {
    bottom: 10px;
  }
}

@keyframes MoveDownUp {

  0%,
  100% {
    top: 10px;
  }

  50% {
    top: 20px;
  }
}
</style>