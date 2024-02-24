<template>
    <div v-if="guest === undefined" class="name-input-container">
      <div class="name-input-form">
        <p>Wie mogen we ontvangen?</p>
        <input class="name-input" type="text" placeholder="Voornaam" v-model="firstName"/>
        <input class="name-input" type="text" placeholder="Achternaam" v-model="lastName"/>
        <button class="button" @click="setName()">Go</button>
      </div>
    </div>
    <div v-else class="timeline-container">
      <div class="welcome" id="welcome">
        <p>Welkom {{ firstName }},</p>
        <p>We ontvangen jou <span v-if="guest.partner">en {{ guest.partner }}</span> graag om samen ons huwelijk te vieren.</p>
      </div>
      <component v-for="event in guest.events" :key="event" :is="event"></component>
      <div class="arrow-down-container">
          <div class="arrow" @click="scrollDown()">
            <font-awesome-icon icon="fa-solid fa-arrow-down" class="icon" />
          </div>
        </div>
    </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import Burgerlijke from '../components/timeline/Burgerlijke.vue';

const burgerlijkeComponent = Burgerlijke;
const receptieComponent = "Receptie";
const ceremonieComponent = "Ceremonie";
const dinerComponent = "Diner";
const feestComponent = "Feest";

const guests = [
    {
        "name": "Gert Van der Brempt",
        "partner": "Nina",
        "events": [
          burgerlijkeComponent,
          receptieComponent,
          ceremonieComponent,
          dinerComponent,
          feestComponent
        ]
    },
    {
        "name": "Nina Steenberghs",
        "events": [
          burgerlijkeComponent,
          receptieComponent,
          ceremonieComponent,
          dinerComponent,
          feestComponent
        ]
    }
  ]

export default {
  name: 'TimelinePage',
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
        "feest"
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
    },
    scrollDown() {
      this.currentScrollId = this.currentScrollId++ % this.scrollIds.length;
      console.log(this.currentScrollId);
      window.location.hash = this.scrollIds[this.currentScrollId];
    }
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
}

.timeline-container {
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  position: relative;
  overflow-y: scroll;
  overflow-x: hidden
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
  background-color: white;
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