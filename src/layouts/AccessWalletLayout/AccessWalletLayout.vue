<template>
  <div>
    <access-my-wallet-container></access-my-wallet-container>
    <price-bar :v-if="online"></price-bar>
    <faqs></faqs>
  </div>
</template>

<script>
export default {
  name: 'AccessWalletContainer',
  data () {
    return {
      online: true
    }
  },
  methods: {
    getRates: async function () {
      const rates = await fetch('http://still-waters-52916.herokuapp.com/ticker').then((res) => {
        return res.json()
      }).catch((err) => {
        return err
      })
      return rates
    }
  },
  mounted: function () {
    const self = this
    const protocol = window.location.protocol
    if (protocol !== 'http:' || protocol !== 'https:') {
      self.online = false
    }
    self.getRates() ? self.online = true : self.online = false
  }
}
</script>

<style lang="scss" scoped>
  @import "AccessWalletLayout.scss";
</style>