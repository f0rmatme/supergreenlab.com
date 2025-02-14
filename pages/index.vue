<!--
      Copyright (C) 2019  SuperGreenLab <towelie@supergreenlab.com>
      Author: Constantin Clauzel <constantin.clauzel@gmail.com>

      This program is free software: you can redistribute it and/or modify
      it under the terms of the GNU General Public License as published by
      the Free Software Foundation, either version 3 of the License, or
      (at your option) any later version.

      This program is distributed in the hope that it will be useful,
      but WITHOUT ANY WARRANTY; without even the implied warranty of
      MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
      GNU General Public License for more details.

      You should have received a copy of the GNU General Public License
      along with this program.  If not, see <http://www.gnu.org/licenses/>.
 -->

<template>
  <section :id="$style.container">
    <div :id='$style.header'>
      <Header responsiveHide='true' />
    </div>
    <div :id='$style.body'>
      <div id='top'></div>
      <Top ref='top' />
      <div id='use-steps'></div>
      <UseSteps ref='use-steps' />
      <Stealth ref='stealth' />
      <BundleIntro ref='bundle-intro' />
      <div :id='$style.title'>
        <SectionTitle title='Welcome to the shop'
            green='Checkout our bundles'
            separator='true'/>
      </div>
      <div :id='$style.shop'></div>
      <div :class='$style.bundle' v-for='b in bundles'>
        <div :id='b.ref'></div>
        <Bundle v-bind='b' :promodiscount='promo.discount' />
      </div>
    </div>
    <Footer />
    <transition name="popup">
      <Promocode v-if='showPopup' :onClose='closePopup' />
    </transition>
  </section>
</template>

<script>
import Header from '~/components/header.vue'
import Top from '~/components/homesection-top.vue'
import UseSteps from '~/components/homesection-use-steps.vue'
import Stealth from '~/components/homesection-stealth-build.vue'
import BundleIntro from '~/components/homesection-bundle-intro.vue'
import Bundle from '~/components/homesection-bundle.vue'
import SectionTitle from '~/components/sectiontitle.vue'
import Footer from '~/components/homesection-footer.vue'
import Promocode from '~/components/overlay-promocode.vue'

import { bundles, shopify, } from '../config.json'

export default {
  components: { Header, SectionTitle, Top, UseSteps, Stealth, BundleIntro, Bundle, Footer,  Promocode,},
  data() {
    return {
      showPopup: false,
    }
  },
  created () {
    window.addEventListener('scroll', this.handleScroll);
  },
  destroyed () {
    if (this.timeout) clearTimeout(this.timeout)
    window.removeEventListener('scroll', this.handleScroll);
  },
  mounted() {
    if (this.$store.state.checkout.promocode.value) return
    const nVisits = parseInt(window.localStorage.getItem('nVisits') || '1')
    window.localStorage.setItem('nVisits', nVisits+1)
    if (nVisits > 1) {
      setTimeout(() => this.$data.showPopup = true, 2000)
    }
    fbq('track', 'ViewContent')
  },
	computed: {
		bundles() {
			return bundles
		},
    promo() {
      const { promos } = shopify,
            promocode = this.$store.state.checkout.promocode.value
      if (!promocode || !promos[promocode]) return {promocode: '', discount: 0}
      return {promocode, discount: promos[promocode]}
    },
    totaldiscount() {
      const bundle = this.bundle,
            promo = this.promo
      return parseInt((1 - (1-bundle.discount/100) * (1-promo.discount/100) ) * 100)
    },
	},
  methods: {
    closePopup() {
      this.$data.showPopup = false
    },
    handleScroll(e) {
      if (this.timeout) clearTimeout(this.timeout)
      this.timeout = setTimeout(() => {
        Object.keys(this.$refs).forEach((name) => {
          if (this.lastEvent == name) {
            return;
          }
          const ref = this.$refs[name],
                { y, height } = ref.$el.getBoundingClientRect(),
                centery = y + height / 2,
                winh = window.innerHeight

          if (centery > winh / 4 && centery < winh * 3/4) {
            this.$matomo && this.$matomo.trackEvent('front-page', 'scrollto', name)
            this.lastEvent = name
          }
        })
      }, 250)
    },
  },
}
</script>

<style module lang=stylus>

#container
  display: flex
  width: 100%
  flex-direction: column
  justify-content: center
  align-items: center

#header
  position: fixed
  width: 100%
  top: 0 
  left: 0
  z-index: 1000

#body
  width: 100%
  max-width: 900pt

#title
  margin: 20pt 0 20pt 0

.separator
  height: 2pt
  margin: 30pt 0
  background-color: #efefef

#shop
  height: 150pt
  margin: 30pt
  background-image: url('~assets/img/shop.svg')
  background-position: center
  background-repeat: no-repeat
  background-size: contain

.bundle
  margin: 0 0 30pt 0

</style>
