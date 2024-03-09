<template>
    <div v-if="guest === undefined" class="welcome-container">
        <div class="welcome-countdown-container">
            <div  v-if="!isMobile" style="padding-top: -4rem;">
                <Countdown></Countdown>
            </div>
            <CountdownMobile v-else></CountdownMobile>
            <p class="welcome-text fancy">Welkom</p>
        </div>
        <div id="name-input" class="name-input-container">
            <div class="name-input-form">
                <p class="fancy">Nina en Gert</p>
                <p>nodigen u uit om samen hun huwelijk te vieren</p>
                <p style="margin-top: 0.5rem;">Wie mogen we ontvangen?</p>
                <input class="name-input" type="text" placeholder="Voornaam" v-model="firstName"/>
                <input class="name-input" type="text" placeholder="Achternaam" v-model="lastName"/>
                <button class="button" @click="setName()">Verder</button>
                <p v-if="noGuestFound" style="font-weight: bold; color: red;">Oeps, we hebben je naam niet terug gevonden, probeer je naam zoals hij op de envelop is geschreven of probeer een met de naam van je partner. Lukt het nog niet? Stuur dan alstublieft een mailtje naar gert.nina.vdbstb@gmail.com</p>
            </div>
        </div>
        <div v-if="!scrolledToNameInput" class="arrow-down-container">
          <div class="arrow" :class="currentScrollId === 0 ? 'white' : ''" @click="scrollToNameInput()">
            <font-awesome-icon icon="fa-solid fa-arrow-down" class="icon" />
          </div>
        </div>
    </div>
    <div v-else class="timeline-container">
      <div v-if="currentScrollId > 0" class="arrow-up-container">
        <div class="arrow" @click="scrollUp()">
          <font-awesome-icon icon="fa-solid fa-arrow-up" class="icon" />
        </div>
      </div>
      <div class="stupid-image-container">
            <img class="stupid-image" src="../assets/img.png">
        </div>
      <div class="welcome" id="welcome">
        <h2>Welkom {{ guest.name.split(" ")[0] }},</h2>
        <p style="margin-top: 0.5rem;">We ontvangen jou <span v-if="partner">en {{ partner.name.split(" ")[0] !== 'Partner' ? partner.name.split(" ")[0] : 'jouw partner' }}</span> graag om samen ons huwelijk te vieren</p>
        <p style="margin-top: 2rem;">Gebruik de pijltjes boven - en onder de pagina om een kijkje te nemen op onze site.</p>
        <p>Je vind hier meer details over het programma en praktische informatie.</p>
        <p>  <span style="font-weight: bold;">Aan het einde vind je een formulier om jou <span v-if="partner">en je partners</span> aanwezigheid te bevestigen</span></p>
        <div class="index">
          <h2>Ga snel naar</h2>
          <p class="index-item" @click="scrollTo(1)">> Het programma</p>
          <p class="index-item" @click="scrollTo(6)" v-if="guest.formType !== 'receptie'">> De praktische informatie</p>
          <p class="index-item" @click="scrollTo(7)">> Je aanwezigheid bevestigen</p>
        </div>
      </div>
      <div class="event-container">
        <component v-for="event in guest.events" :key="event" :is="event"></component>
        <div id="form" class="container">
          <Form :for-partner="false" @submit="() => { if (partner) scrollDown();}" :guest="guest"></Form>
        </div>
        <div v-if="partner" id="form_partner" class="container">
          <Form :for-partner="true" :guest="partner"></Form>
        </div>
      </div>
      <div v-if="currentScrollId !== scrollIds.length - (partner ? 1 : 2)" class="arrow-down-container">
          <div class="arrow" :class="{'white': currentScrollId === 0}" @click="scrollDown()">
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
import CountdownMobile from '../components/register/CountdownMobile.vue';
import Countdown from '../components/register/Countdown.vue';

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
    burgerlijkeComponent,
    ceremonieComponent,
    dinerComponent,
    feestComponent,
    faqComponent
  ],
  partial: [
    burgerlijkeComponent,
    ceremonieComponent,
    feestComponent,
    faqComponent
  ],
  receptie: [
    burgerlijkeComponent,
    receptieComponent,
    faqComponent
  ],
  ceremonie: [
    burgerlijkeComponent,
    receptieComponent,
    ceremonieComponent,
    faqComponent
  ]
}

const guests = [
    // All
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
    {
        "name": "Dieter Dedecker",
        "partner": "Ann Steenberghs",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Ann Steenberghs",
        "partner": "Dieter Dedecker",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Piet Steenberghs",
        "partner": "Sabine Hendrickx",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Sabine Hendrickx",
        "partner": "Piet Steenberghs",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Aaron Hamerlynck",
        "partner": "Kaat Van der Brempt",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Kaat Van der Brempt",
        "partner": "Aaron Hamerlynck",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Robbe Van der Brempt",
        "partner": "Stephen Hunt",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Stephen Hunt",
        "partner": "Robbe Van der Brempt",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Arne Van Der Perren",
        "partner": "Silke Van der Brempt",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Silke Van der Brempt",
        "partner": "Arne Van Der Perren",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "An Verstrepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Hans Steenberghs",
        "partner": "Evelien Lefebure",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Evelien Lefebure",
        "partner": "Hans Steenberghs",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Koen Steenberghs",
        "partner": "Claudine Verhoeven",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Claudine Verhoeven",
        "partner": "Koen Steenberghs",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Lennart Steenberghs",
        "partner": "Isabella",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Isabella",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Laurens Vandenbussche",
        "partner": "Loes Steenberghs",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Loes Steenberghs",
        "partner": "Laurens Vandenbussche",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Brent Verhasselt",
        "partner": "Glynis Van Eyken",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Glynis Van Eyken",
        "partner": "Brent Verhasselt",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Frans Verstrepen",
        "partner": "Michelle Cnop",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Michelle Cnop",
        "partner": "Frans Verstrepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Marleen Verstrepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Rik Verstrepen",
        "partner": "Jelle Van Den Heede",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Jelle Van Den Heede",
        "partner": "Rik Verstrepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Borja Casanova",
        "partner": "Karla Tavárez",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Karla Tavárez",
        "partner": "Borja Casanova",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Carlo Kriekels",
        "partner": "Wendy Kriekels",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Wendy Kriekels",
        "partner": "Carlo Kriekels",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Pedro Tavárez",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Volcker Wiest",
        "partner": "Tina Kern",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Tina Kern",
        "partner": "Volcker Wiest",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Patrick Reynders",
        "partner": "Patricia Zeelmaekers",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Patricia Zeelmaekers",
        "partner": "Patrick Reynders",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Lelly Knaepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Clemy Knaepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Clementine Knaepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Niny Knaepen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Jos Vandormael",
        "partner": "Goverdine Hermans",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Goverdine Hermans",
        "partner": "Jos Vandormael",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Dina Hermans",
        "partner": "Jos Vandormael",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Pia Buntinx",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Jaak Bussels",
        "partner": "Annemie Verlinden",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Annemie Verlinden",
        "partner": "Jaak Bussels",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Koen Gielen",
        "partner": "Rika Bauduin",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Rika Bauduin",
        "partner": "Koen Gielen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Bart Vandeloo",
        "partner": "Carine Vandyck",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Carine Vandyck",
        "partner": "Bart Vandeloo",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Stefan Verellen",
        "partner": "Els Boyen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Els Boyen",
        "partner": "Stefan Verellen",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Steve Dhoore",
        "partner": "Lavigna Wouters",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Lavigna Wouters",
        "partner": "Steve Dhoore",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Frank Wellens",
        "partner": "Kathleen Wens",
        "formType": "all",
        "events": eventGroups.all
    },
    {
        "name": "Kathleen Wens",
        "partner": "Frank Wellens",
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
        "name": "Dino Margullier",
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
    {
        "name": "Jef Somers",
        "partner": "Nathalie Sellekaerts",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Nathalie Sellekaerts",
        "partner": "Jef Somers",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Evert Baetens",
        "partner": "Ann Hernalsteens",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Ann Hernalsteens",
        "partner": "Evert Baetens",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Dries Van Itterbeeck",
        "partner": "Kevin Munten",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Kevin Munten",
        "partner": "Dries Van Itterbeeck",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Hendrik Vandenberghe",
        "partner": "Frauke Goovaerts",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Frauke Goovaerts",
        "partner": "Hendrik Vandenberghe",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Frederik Vercammen",
        "partner": "Julie De Doncker",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Julie De Doncker",
        "partner": "Frederik Vercammen",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Els Vochten",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Simon Wauters",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Willy De Munck",
        "partner": "Myriam Buggenhout",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Myriam Buggenhout",
        "partner": "Willy De Munck",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Johan Heyvaerts",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Lieven Mertens",
        "partner": "Ann De Mulder",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Ann De Mulder",
        "partner": "Lieven Mertens",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Nadia Sonck",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Oliver Krsteski",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Lien Demulder",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Koen Raymaekers",
        "partner": "Laure Verhaegen",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Laure Verhaegen",
        "partner": "Koen Raymaekers",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Fleur Van Gils",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Emke Op 't Eynde",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Camille Persyn",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Tom Bossuyt",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Yaro Debeer",
        "partner": "Loike Jacobs",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Loike Jacobs",
        "partner": "Yaro Debeer",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Nicolas Grootjans",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Wouter Janssens",
        "partner": "Elodie Derie",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Elodie Derie",
        "partner": "Wouter Janssens",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Johannes Mevis",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Samuel Vermote",
        "partner": "Martha Pickles",
        "formType": "full",
        "events": eventGroups.full
    },
    {
        "name": "Martha Pickles",
        "partner": "Samuel Vermote",
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
    {
        "name": "Evi Vermandere",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Benjamin Vermeulen",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Cid Dedecker",
        "partner": "Romy Schrey",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Romy Schrey",
        "partner": "Cid Dedecker",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Dante Dedecker",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Finn Dedecker",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Gus Dedecker",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Leon Dedecker",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Maud Dedecker",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Pieter-Jan Dorpmans",
        "partner": "Ella Steenberghs",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Ella Steenberghs",
        "partner": "Pieter-Jan Dorpmans",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Sam Kerkhofs",
        "partner": "Sophie M'Sallem",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Sophie M'Sallem",
        "partner": "Sam Kerkhofs",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Zeb Lemmens",
        "partner": "Lana Steenberghs",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Lana Steenberghs",
        "partner": "Zeb Lemmens",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Pieter Peeters",
        "partner": "Gitte Kerkhofs",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Gitte Kerkhofs",
        "partner": "Pieter Peeters",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Mae Peeters",
        "partner": "Nelson Peeters",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Nelson Peeters",
        "partner": "Mae Peeters",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Kaat Steenberghs",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Jeremy Bouillon",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Flor Cloetens",
        "partner": "Rebecca van den Berg",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Rebecca van den Berg",
        "partner": "Flor Cloetens",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Seppe Cloetens",
        "partner": "Sarah Moreno",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Sarah Moreno",
        "partner": "Seppe Cloetens",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Bram Heylen",
        "partner": "Elisabeth De Grave",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Elisabeth De Grave",
        "partner": "Bram Heylen",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Louis Kips",
        "partner": "Zoë Somers",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Zoë Somers",
        "partner": "Louis Kips",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Jeroen Lami",
        "partner": "Lieze Moutoul",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Lieze Moutoul",
        "partner": "Jeroen Lami",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Pepijn Seys",
        "partner": "Marie Silverans",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Marie Silverans",
        "partner": "Pepijn Seys",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Thibaut Seys",
        "partner": "Robine Silverans",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Robine Silverans",
        "partner": "Pepijn Seys",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Wouter De Naeyer",
        "partner": "An-Sofie Wouters",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "An-Sofie Wouters",
        "partner": "Wouter De Naeyer",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Yentl Koopmans",
        "partner": "Joost Slegers",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Joost Slegers",
        "partner": "Yentl Koopmans",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Leni Raemen",
        "partner": "Matthias Roobroeck",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Matthias Roobroeck",
        "partner": "Leni Raemen",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Laura Dewitte",
        "partner": "Simon Oeyen",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Simon Oeyen",
        "partner": "Laura Dewitte",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Eline Camerman",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Adriaan Moeys",
        "partner": "Karlien Demol",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Karlien Demol",
        "partner": "Adriaan Moeys",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Alicia Ramos",
        "partner": "Brian Ramos",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Brian Ramos",
        "partner": "Alicia Ramos",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Marco Vandamme",
        "partner": "Sofie Hendrix",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Sofie Hendrix",
        "partner": "Marco Vandamme",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Mano Vandeput",
        "partner": "Maarten Meulemans",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Maarten Meulemans",
        "partner": "Mano Vandeput",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Ruben Michaux",
        "partner": "Thibo Pinte",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Thibo Pinte",
        "partner": "Ruben Michaux",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Laura Peeters",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Lauren Adriaenssens",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Dieter Holvoet",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Willem Mevis",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Fien Van Meerbeek",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Jan Van Roy",
        "partner": "Hanne Decaluwe",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Hanne Decaluwe",
        "partner": "Jan Van Roy",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Jan De Beukeleer",
        "partner": "Mounia Faid",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Mounia Faid",
        "partner": "Jan De Beukeleer",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Walter Struyf",
        "partner": "Sandra Budé",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Sandra Budé",
        "partner": "Walter Struyf",
        "formType": "partial",
        "events": eventGroups.partial
    },
    {
        "name": "Guido Van Kriekinge",
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
    {
        "name": "Kristof Grootvriendt",
        "partner": "Caroline Remory",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Caroline Remory",
        "partner": "Kristof Grootvriendt",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Caroline Goethals",
        "partner": "Jan Van Oost",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jan Van Oost",
        "partner": "Caroline Goethals",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Lennart Smets",
        "partner": "Ester Vylders",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ester Vylders",
        "partner": "Lennart Smets",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Tim Ulens",
        "partner": "Liesbet Pluym",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Liesbet Pluym",
        "partner": "Tim Ulens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kristof Van Der Snick",
        "partner": "Naomi Mesotten",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Naomi Mesotten",
        "partner": "Kristof Van Der Snick",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Sylvie Dubois",
        "partner": "Partner Sylvie Dubois",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Sylvie Dubois",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Godwina Mylle",
        "partner": "Dirk",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Dirk",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Leentje Eeckhout",
        "partner": "Jo",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jo",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Roger Aertsens",
        "partner": "Agnes Aertsens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Agnes Aertsens",
        "partner": "Roger Aertsens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Peter Aertsens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Erik Baptist",
        "partner": "Partner Erik Baptist",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Erik Baptist",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Sven Baten",
        "partner": "Ilse Cuypers",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ilse Cuypers",
        "partner": "Sven Baten",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Tuur Bax",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Reggie Beyaert",
        "partner": "Partner Reggie Beyaert",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Reggie Beyaert",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Rik Bobbaers",
        "partner": "Klaartje Smeets",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Klaartje Smeets",
        "partner": "Rik Bobbaers",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Karlo Bogaerts",
        "partner": "Ann Philips",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ann Philips",
        "partner": "Karlo Bogaerts",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Bart Bollen",
        "partner": "Carine Lietaer",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Carine Lietaer",
        "partner": "Bart Bollen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Peter Bouts",
        "partner": "Partner Peter Bouts",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Peter Bouts",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Dirk Broeckx",
        "partner": "Ingrid Kums",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ingrid Kums",
        "partner": "Dirk Broeckx",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kurt Bruggeman",
        "partner": "Jill Van Vaeck",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jill Van Vaeck",
        "partner": "Kurt Bruggeman",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Marc Collier",
        "partner": "Myleen Christiaens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Myleen Christiaens",
        "partner": "Marc Collier",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Mabel Vanasbroeck",
        "partner": "Johan Vanasbroeck",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Johan Vanasbroeck",
        "partner": "Mabel Vanasbroeck",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ann Goethals",
        "partner": "Olivier Vanbellegem",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Olivier Vanbellegem",
        "partner": "Ann Goethals",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Yves Vandemeutter",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Robbie Craenen",
        "partner": "Christel Cravillon",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Christel Cravillon",
        "partner": "Robbie Craenen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Guy Croes",
        "partner": "Amanda Bauduin",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Amanda Bauduin",
        "partner": "Guy Croes",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Genti Çupi",
        "partner": "Partner Genti Çupi",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Genti Çupi",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Frederik de Kriek",
        "partner": "Inge Wullaert",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Inge Wullaert",
        "partner": "Frederik de Kriek",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kris De Lepeleire",
        "partner": "Annemie Celis 1",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Annemie Celis 1",
        "partner": "Kris De Lepeleire",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Steven De Preter",
        "partner": "Sylvia Lescrauwaet",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Sylvia Lescrauwaet",
        "partner": "Steven De Preter",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Luc De Temmerman",
        "partner": "Ann-Marie Uyttersprot",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ann-Marie Uyttersprot",
        "partner": "Luc De Temmerman",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Paul Dekeyser",
        "partner": "Hilde Hertecant",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Hilde Hertecant",
        "partner": "Paul Dekeyser",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Leen Delbeke",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Luc Dewolf",
        "partner": "Renilde Doms",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Renilde Doms",
        "partner": "Luc Dewolf",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Marc Dillen",
        "partner": "Ann Claes",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ann Claes",
        "partner": "Marc Dillen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Katia Doornaert",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jo Driessen",
        "partner": "Anne-Mie De Nève",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Anne-Mie De Nève",
        "partner": "Jo Driessen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Michele Driessen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Miet Driessen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Michel Dubois",
        "partner": "Marianne Vermeylen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Marianne Vermeylen",
        "partner": "Michel Dubois",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Charly Fondu",
        "partner": "Hilde Allegaert",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Hilde Allegaert",
        "partner": "Charly Fondu",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Frederik Gelaude",
        "partner": "Marjan Belsack",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Marjan Belsack",
        "partner": "Frederik Gelaude",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Renilde Gielen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jan Goemans",
        "partner": "Caroline Vanderhallen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Caroline Vanderhallen",
        "partner": "Jan Goemans",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Karolien Haepers",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Georges Haeyen",
        "partner": "Josine",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Josine",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Herwig Holsteyns",
        "partner": "Inge Heynderickx",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Inge Heynderickx",
        "partner": "Herwig Holsteyns",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Werner Huygen",
        "partner": "Sophie Tournier",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Sophie Tournier",
        "partner": "Werner Huygen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Richard Indesteege",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Koen Jackers",
        "partner": "Annegret Beckers",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Annegret Beckers",
        "partner": "Koen Jackers",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Koen Jacobs",
        "partner": "Annemie Celis",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Annemie Celis",
        "partner": "Koen Jacobs",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Geert Joosten",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Peter Kessels",
        "partner": "Griet Flamez",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Griet Flamez",
        "partner": "Peter Kessels",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Stef Knaepen",
        "partner": "Renilde Nihoul",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Renilde Nihoul",
        "partner": "Stef Knaepen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kris Lefebure",
        "partner": "Kristel Broekmans",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kristel Broekmans",
        "partner": "Kris Lefebure",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Paul Lemmens",
        "partner": "Anne Dewaele",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Anne Dewaele",
        "partner": "Paul Lemmens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Gert-Jan Lenaerts",
        "partner": "Karolien Jochmans",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Karolien Jochmans",
        "partner": "Gert-Jan Lenaerts",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Stefaan Lettens",
        "partner": "Ingrid Govaerts",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ingrid Govaerts",
        "partner": "Stefaan Lettens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jo Maesen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Wim Mertens",
        "partner": "Ann",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ann",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Veronique Missotten",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Hans Nackaerts",
        "partner": "Sara Philips",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Sara Philips",
        "partner": "Hans Nackaerts",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Anton Ndoj",
        "partner": "Partner Anton Ndoj",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Anton Ndoj",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Bob Nyssen",
        "partner": "Kris Keymolen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kris Keymolen",
        "partner": "Bob Nyssen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Alex Parmentier",
        "partner": "Veerle Carron",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Veerle Carron",
        "partner": "Alex Parmentier",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Bernard Peeters",
        "partner": "Dédé Roodhooft",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Dédé Roodhooft",
        "partner": "Bernard Peeters",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Joris Peeters",
        "partner": "Sofie Debacker",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Sofie Debacker",
        "partner": "Joris Peeters",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Thomas Peperstraete",
        "partner": "Annelies De Blauwe",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Annelies De Blauwe",
        "partner": "Thomas Peperstraete",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Mark Robyns",
        "partner": "Isabel Verlinden",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Isabel Verlinden",
        "partner": "Mark Robyns",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Herwig Rogiers",
        "partner": "Joëlle Vaes",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Joëlle Vaes",
        "partner": "Herwig Rogiers",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Isabelle Ronse",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Olivier Schmitz",
        "partner": "Renée Schoups",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Renée Schoups",
        "partner": "Olivier Schmitz",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Tom Schoors",
        "partner": "Dorien Helsen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Dorien Helsen",
        "partner": "Tom Schoors",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Werner Smets",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jan Swennen",
        "partner": "Ann Op de Beek",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ann Op de Beek",
        "partner": "Jan Swennen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Stef Thulie",
        "partner": "Ingrid Peters",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ingrid Peters",
        "partner": "Stef Thulie",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Dries Trippas",
        "partner": "Partner Dries Trippas",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Dries Trippas",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Wilfried Van Lishout",
        "partner": "Sophie Rappoort",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Wilfried Van Lishout",
        "partner": "Sophie Rappoort",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Gert Vandeurzen",
        "partner": "Tal Vanaken",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Tal Vanaken",
        "partner": "Gert Vandeurzen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Mark Vandeurzen",
        "partner": "Suzy",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Suzy",
        "partner": "Mark Vandeurzen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Amie Van Hool",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Charlotte Mercier",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Geert Vanlaecke",
        "partner": "Kathleen Lamine",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kathleen Lamine",
        "partner": "Geert Vanlaecke",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Pascal Vanovermeire",
        "partner": "Brigitte Vanhoutte",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Brigitte Vanhoutte",
        "partner": "Pascal Vanovermeire",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Johan Vanpée",
        "partner": "Renilde Vos",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Renilde Vos",
        "partner": "Johan Vanpée",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Karl Vansteenkiste",
        "partner": "Kaat Vervaecke",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Kaat Vervaecke",
        "partner": "Karl Vansteenkiste",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Peter Verbeek",
        "partner": "Annemie Gielen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Annemie Gielen",
        "partner": "Peter Verbeek",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jef Verdonck",
        "partner": "Christine Vergallen",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Christine Vergallen",
        "partner": "Jef Verdonck",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Walter Verlinden",
        "partner": "Ann Meyers",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ann Meyers",
        "partner": "Walter Verlinden",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Anne Vermeersch",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Nicolaas Viets",
        "partner": "Laetitia Bot",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Laetitia Bot",
        "partner": "Nicolaas Viets",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Yves Vleminckx",
        "partner": "Monique Ulens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Monique Ulens",
        "partner": "Yves Vleminckx",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ndue Vorfi",
        "partner": "Partner Ndue Vorfi",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Ndue Vorfi",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Hilde Waes",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Mieke Willems",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Frrok Vorfi",
        "partner": "Partner Frrok Vorfi",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Partner Frrok Vorfi",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Ruben De Clippel",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Steven De Pauw",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Gentiana Gorreja",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Jasmijn Nuyts",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Tom Vananderoye",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Isabel De Cavel",
        "formType": "receptie",
        "events": eventGroups.receptie
    },
    {
        "name": "Joanna Lemmens",
        "formType": "receptie",
        "events": eventGroups.receptie
    },

    // Ceremonie
    {
        "name": "Jean-Louis De Lagausie",
        "partner": "Irene Bien",
        "formType": "ceremonie",
        "events": eventGroups.ceremonie
    },
    {
        "name": "Irene Bien",
        "partner": "Jean-Louis De Lagausie",
        "formType": "ceremonie",
        "events": eventGroups.ceremonie
    },
    {
        "name": "Hubert Surinx",
        "partner": "Cecile Vandormael",
        "formType": "ceremonie",
        "events": eventGroups.ceremonie
    },
    {
        "name": "Cecile Vandormael",
        "partner": "Hubert Surinx",
        "formType": "ceremonie",
        "events": eventGroups.ceremonie
    },

  ]

export default {
  name: 'TimelinePage',
  components: {
    FAQ,
    Form,
    Countdown,
    CountdownMobile
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
      currentScrollId: 0,
      noGuestFound: false,
      scrolledToNameInput: false,
    }
  },
  methods: {
    setName() {
      this.noGuestFound = false;
      localStorage.setItem('guest_first_name', this.firstName);
      localStorage.setItem('guest_last_name', this.lastName);
      this.getGuest(this.firstName + ' ' + this.lastName);
      window.location.hash = this.scrollIds[this.currentScrollId];
    },
    getGuest(name) {
      this.guest = guests.find((el) => {
        return el.name.toLowerCase() === name.toLowerCase();
      });
      if (this.guest && this.guest.partner) {
        this.partner = guests.find((el) => {
          return el.name.toLowerCase() === this.guest.partner.toLowerCase();
        });
      } else {
        this.noGuestFound = true;
      }
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
        element.scrollIntoView({
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
        element.scrollIntoView({
              behavior: 'smooth'
          });
      } else {
        this.scrollDown();
      }
    },
    scrollToNameInput() {
      this.scrolledToNameInput = true;
      const element = document.querySelector("#name-input");
      if (element) {
        element.scrollIntoView({
              behavior: 'smooth'
          });
      }
    }
  },
  mounted() {
    if (localStorage.getItem('guest_first_name') && localStorage.getItem('guest_last_name')) {
      this.firstName = localStorage.getItem('guest_first_name');
      this.lastName = localStorage.getItem('guest_last_name');
      this.setName();
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

.timeline-container {
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  position: relative;
  overflow-y: hidden;
  position: relative;
  overflow-x: hidden
}

.welcome-container {
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  position: relative;
  overflow-y: hidden;
  overflow-x: hidden
}

.name-input-container {
  padding: 2rem;
  height: 100vh;
  display: flex;
  justify-content: center;
  background-color: #ebebeb;
  color: #39393A !important;
  overflow-y: auto;
}

.welcome-countdown-container {
  position: relative;
  height: 100vh;
}

.fancy {
    font-size: 3rem;
    font-family: 'Brittany', sans-serif;
}

.welcome-text {
    font-size: 2rem;
  position: absolute;
  width: 100%;
  text-align: center;
  bottom: 6rem;
  height: 10px;
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

.name-input-form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  place-self: center;
  width: 400px;
}

.welcome {
  padding: 2rem;
  padding-top: 6rem;
  height: 100%;
  position: relative;
  z-index: 5;
  display: flex;
  flex-direction: column;
  justify-content: start;
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
    background-color: #68121B;
    border-color: #68121B;
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

.stupid-image-container {
    position: absolute;
    height: 50vh;
    left: 50%;
    bottom: -3rem;
    z-index: 0;
    transform: translate(-50%, 0);
    display: flex;
    justify-content: center;
}

.border-image-right {
    position: absolute;
    height: 8.5rem;
    width: 1px;
    left: 37.5%;
    bottom: 0;
    transform: translate(-50%, 0);
    background-color: #995116;
}

.border-image-left {
    position: absolute;
    height: 8.3rem;
    left: 62.5%;
    width: 1px;
    bottom: 0;
    transform: translate(-50%, 0);
    background-color: #995116;
}

.stupid-image {
    width: 100%;
    object-fit: contain;

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

.white {
    background-color: white;

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

  .stupid-image-container {
    width: 100vw;
    height: auto;
    opacity: 50%;
    left: 50%;
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