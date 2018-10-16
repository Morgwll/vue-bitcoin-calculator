<template>
  <div id="app">
    <app-banner :mainTitle="mainTitle" :mainBlurb="mainBlurb"/>
    <app-calculator/>
  </div>
</template>
<script>
import appCalculator from './components/Calculator.vue';
import appBanner from './components/Banner.vue';
export default {
  components: {
    appCalculator,
    appBanner
  },
  data: () => ({
    mainTitle: 'BitCoin Calculator',
    mainBlurb: 'Enter how many BitCoins you want to buy and it will tell you the price in Pounds'
  })
}
</script>
<style lang="scss">
@import './scss/variables';
html {
  background-image: url('../assets/chart.jpg');
  width: 100%;
  font-family: 'Chakra Petch', sans-serif;
  text-shadow: 0 0 3px $black, 0 0 5px $black;
  background-size: cover;
  background-position-x: center;
  body {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    color: $light-grey;
    input:focus,
    select:focus,
    textarea:focus,
    button:focus {
        outline: none;
    }
  }
}
</style>