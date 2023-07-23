<template>
  <div v-if="componentIndex > 0" class="arrow-up-container">
    <div class="arrow" @click="cycleComponent(-1)">
      <font-awesome-icon icon="fa-solid fa-arrow-up" class="icon" />
    </div>
  </div>
  <div class="carousel-container">
    <Transition :name="transition">
      <div class="component-container" :key="componentIndex">
        <component :is="components[componentIndex]">
        </component>
      </div>
    </Transition>
  </div>
  <div v-if="componentIndex < components.length - 1" class="arrow-down-container">
    <div class="arrow" @click="cycleComponent(1)">
      <font-awesome-icon icon="fa-solid fa-arrow-down" class="icon" />
    </div>
  </div>
</template>

<script>
/* eslint-disable vue/no-unused-components */
import Countdown from './Countdown.vue';
import HotelInfo from './HotelInfo.vue';
import HotelInfoMobile from './HotelInfoMobile.vue';
import CountdownMobile from './CountdownMobile.vue';
import AdressForm from './AdressForm.vue';
import AdressFormMobile from './AdressFormMobile.vue';

export default {
  name: 'VerticalCarousel',
  components: {
    Countdown,
    HotelInfo,
    HotelInfoMobile,
    CountdownMobile,
    AdressForm,
    AdressFormMobile,
  },
  props: [
    'components'
  ],
  data() {
    return {
      componentIndex: 0,
      transition: "slide-up",
      scrollLock: false,
    }
  },
  methods: {
    onScroll(event) {
      if (!this.scrollLock) {
        const scrollDir = event.deltaY;
        this.scrollLock = true;
        if (scrollDir > 0) {
          console.log('up');
          this.cycleComponent(1);
        }
        else if (scrollDir < 0) {
          console.log('down');
          this.cycleComponent(-1);
        }
        setTimeout(function () {
          this.scrollLock = false;
        }.bind(this), 800);
      }
    },
    cycleComponent(dir) {
      if (dir > 0) {
        this.transition = "slide-up";
        if (this.componentIndex < this.components.length - 1) {
          this.componentIndex++;
        }
      } else if (dir < 0) {
        this.transition = "slide-down";
        if (this.componentIndex > 0) {
          this.componentIndex--;
        }
      }
      // console.log(this.components[this.componentIndex]);
    }
  },
  watch: {
    componentIndex: {
      handler: function () {
        window.addEventListener('wheel', this.onScroll);
      },
      immediate: true,
    }
  },
  computed: {


  },
  mounted() {
  }
}
</script>

<style scoped>
.carousel-container {
  height: 100%;
  width: 100%;
  position: relative;
}

.arrow-down-container {
  z-index: 10;
  position: absolute;
  width: 100%;
  height: 4rem;
  display: flex;
  justify-content: center;
  bottom: 0;
  animation: MoveUpDown 2s linear infinite;
}

.arrow-up-container {
  z-index: 10;
  position: absolute;
  width: 100%;
  height: 4rem;
  display: flex;
  justify-content: center;
  top: 0;
  animation: MoveDownUp 2s linear infinite;
}



.component-container {
  height: 100%;
  width: 100%;
  position: absolute;
  background-color: #ebebeb;
}

.slide-up-leave-active,
.slide-down-leave-active,
.slide-up-enter-active,
.slide-down-enter-active {
  transition: all 0.8s ease-out;
}

.slide-up-enter-from {
  transform: translateY(100%);
}

.slide-up-leave-to {
  transform: translateY(-100%);
}

.slide-down-enter-from {

  transform: translateY(-100%);
}

.slide-down-leave-to {
  transform: translateY(100%);
}

.arrow {
  /* padding: 10px; */
  display: flex;
  justify-content: center;
  background-color: white;
  border-radius: 9999px;
  height: 3rem;
  width: 3rem;
  cursor: pointer;
}

.icon {
  font-size: 2rem;
  place-self: center;
  ;
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
