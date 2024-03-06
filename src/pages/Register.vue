<template>
  <VerticalCarousel :components="components">

  </VerticalCarousel>
</template>

<script>
import VerticalCarousel from '../components/register/VerticalCarousel.vue'

export default {
  name: 'RegisterPage',
  components: {
    VerticalCarousel
  },
  data() {
    return {
      carouselComponents: [
        'Countdown',
        'HotelInfo',
        'AdressForm',
      ]
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
      return this.carouselComponents.map((element) => {
        return element + (this.isMobile ? 'Mobile' : '');
      })
    }
  }
}
</script>
