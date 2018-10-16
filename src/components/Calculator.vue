<template>
  <div class="calculator">
    If you want to buy <input class="calculator__input" v-model="poundEntry" value="1"/> Bitcoins<br>
    it will cost you <span class="calculator__price">£{{ bitcoinValue }}</span>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'vue-bitcoin-calculator',
  data: () => ({
      bitcoinValue: [],
      poundEntry: 1,
      pound: [],
      errors: []
  }),
  watch: {
    poundEntry() {
      let brutValue = this.pound.bpi.GBP.rate;
      brutValue = brutValue.replace(',','');
      let value = parseFloat(brutValue, 8);
      let total = value * this.poundEntry;
      this.bitcoinValue = total;
    }
  },
  created () {
    axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
    .then(response => {
      this.pound = response.data
      this.bitcoinValue = response.data.bpi.GBP.rate
      console.log(response)
    })
    .catch( e => {
      this.errors.push(e)
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import '../scss/variables';
.calculator {
  font-size: 1.5rem;
  width: 100%;
  max-width: 995px;
  margin: 0 auto;
  text-align: center;
  &__input {
    background-color: $dark-transparent;
    border: none;
    color: $light-grey;
    font-size: 2.7rem;
    font-family: 'Chakra Petch', sans-serif;
    text-shadow: 0 0 3px $black, 0 0 5px $black;
    text-align: center;
    border-radius: 3px;
    max-width: 200px;
    &:hover {
      transform: scale(1.1, 1.1);
      transition: .5s;
    }
  }
  &__price {
    font-size: 2.7rem;
    &:hover {
      transform: scale(1.1, 1.1);
    }
  }
}
</style>
