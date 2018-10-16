# vue-bitcoin-calculator
a vue bitcoin calculator excercise for TMW Unlimited

In this exercise I've used Vue.js. I think the approach is clean, lightweight and doesn't require much coding. Most of the time was spent figuring out what font to use, what background, etc. But here is a bit of documentation.

I have left some data in the main `App.vue` file that can be manipulated without having to touch anything directly in the component, in case a CMS like sitecore could make use of those. So they are passed with data bindings.

```
data: () => ({
    mainTitle: 'BitCoin Calculator',
    mainBlurb: 'Enter how many BitCoins you want to buy and it will tell you the price in Pounds'
  })
```

Only the variables have their own scss file. All components generally have their own styling. Force of habit, this way they are more modular, and the file itself refers to the styles it contains and nothing more. Regardless, unless it's specified in the tag itself, the styles will spread around the entire project.

```
<style lang="scss">
@import './scss/variables';
html {
  background-image: url('../assets/chart.jpg');
  width: 100%;
  font-family: 'Chakra Petch', sans-serif;
  text-shadow: 0 0 3px $black, 0 0 5px $black;
  background-size: cover;
  background-position-x: center;
  ...
```

I have used `axios` to fetch the data from the api and store it in an array inside the data element. That is bound to the input fields and they get modified in real time through the `watch` functionality.

```
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
```
Please leave a comment if you are curious about anything else. Would be fun to do something like this but pushing it forward, like adding different currencies, etc.
