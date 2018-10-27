<template>
  <q-page class="flex flex-center">
  <!-- Single Line Input -->
  <q-input stack-label="Currency" v-model="message" placeholder="Gigi" @blur="getPriceForCode" />
    <img alt="Quasar logo" src="~assets/quasar-logo-full.svg">
    {{ info }}
  </q-page>
</template>

<style>
</style>

<script>
import axios from 'axios';

export default {
  name: 'PageIndex',
  data () {
    return {
      info: null,
      message: 'quasar is crazy!'

    }
  },
  mounted () {
    axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(response => (this.info = response.data.bpi));
  },
  methods: {
    getPriceForCode () {
      if (this.message) {
        console.log('Check the price for bitcoin under currency', this.message);
        if (this.message === 'gbp') {
          this.info = this.info.GBP.rate;
        }
      }
    }
  }
}
</script>
