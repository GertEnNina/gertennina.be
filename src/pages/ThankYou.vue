<template>
<div class="thank-you" id="thank-you">
  <div class="content">
    <h2>Bedankt!</h2>
        <p class="bit-bigger" style="margin-top: 0.5rem">Voor het fantastische feest</p>
        <p class="bit-bigger">De mooie wensen</p>
        <p class="bit-bigger" style="margin-bottom: 2rem">En de gulle bijdragen aan een prachtige huwelijksreis!</p>
        <p>Nog wat nagenieten? <a target="_blank" href="https://printshop.jeroenvranckaert.be/-ninagert/gallery">Neem een kijkje naar de foto's</a></p>
      </div>
  </div>
</template>

<style>
  .thank-you {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
  }

  .content {
    align-self: center;
  }

  .bit-bigger {
    font-size: large;
  }
</style>

<script>

export default {
  name: 'ThankYouPage',
  components: {
  },
  data() {
    return {

    }
  },
  computed: {
    isMobile() {
      if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
        return true
      } else {
        return false
      }
    }
  }
}
</script>
