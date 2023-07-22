<template>
  <div class="carousel-container">
    <Transition :name="transition">
      <div class="component-container" :key="componentIndex">
        <component :is="components[componentIndex]">
        </component>
      </div>
    </Transition>
  </div>
</template>

<script>
/* eslint-disable vue/no-unused-components */
import Countdown from './Countdown.vue';
import HotelInfo from './HotelInfo.vue';
import HotelInfoMobile from './HotelInfoMobile.vue';
import CountdownMobile from './CountdownMobile.vue'

export default {
  name: 'VerticalCarousel',
  components: {
    Countdown,
    HotelInfo,
    HotelInfoMobile,
    CountdownMobile
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
          this.transition = "slide-up";
          this.cycleComponent(1);
        }
        else if (scrollDir < 0) {
          this.transition = "slide-down";
          this.cycleComponent(-1);
        }
        setTimeout(function () {
          this.scrollLock = false;
        }.bind(this), 800);
      }
    },
    cycleComponent(dir) {
      if (dir > 0) {
        if (this.componentIndex < this.components.length - 1) {
          this.componentIndex++;
        }
      } else if (dir < 0) {
        if (this.componentIndex > 0) {
          this.componentIndex--;
        }
      }
      console.log(this.components[this.componentIndex]);
    }
  },
  watch: {

  },
  computed: {


  },
  mounted() {
    window.addEventListener('wheel', this.onScroll);
  }
}
</script>

<style scoped>
.carousel-container {
  height: 100%;
  width: 100%;
  position: relative;
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
</style>
