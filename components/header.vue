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
  <section :id='$style.container' :class='responsiveHide ? $style.responsiveHide : ""'>
    <div :id='$style.logo'>
      <Logo subtitle='Growshop.' />
    </div>
    <div :id='$style.menu'>
      <div><nuxt-link @click='onClick' :to="{ path: '/', hash: '#top' }">Home</nuxt-link></div>
      <div><nuxt-link @click='onClick' :to="{ path: '/', hash: '#mono-box-bundle' }">Mono box bundle</nuxt-link></div>
      <div><nuxt-link @click='onClick' :to="{ path: '/', hash: '#multi-box-bundle' }">Multi box bundle</nuxt-link></div>
      <div><nuxt-link @click='onClick' :to="{ path: '/', hash: '#closet-bundle' }">Closet bundle</nuxt-link></div>
      <div><nuxt-link @click='onClick' :to="{ path: '/', hash: '#micro-grow-bundle' }">Microgrow bundle</nuxt-link></div>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/logo.vue'

export default {
  components: { Logo, },
  props: ['responsiveHide',],
  methods: {
    onClick(e) {
      this.$matomo && this.$matomo.trackEvent('front-page-menu', 'click', e.target.href.split('#')[1])
    },
  },
}

</script>

<style module lang=stylus>

#container
  display: flex
  width: 100%
  background-color: rgba(255, 255, 255, 0.8)
  align-items: center
  justify-content: space-between
  padding: 0 0 0 10pt
  @media only screen and (max-width: 600px)
    justify-content: center
    padding: 10pt 0 10pt 0
    font-size: 1.2em

#menu
  display: flex
  font-size: 0.8em
  @media only screen and (max-width: 600px)
      display: none

#menu > div > a
  display: block
  color: #5D5D5D
  font-weight: 600
  cursor: pointer
  padding: 15pt 10pt
  text-decoration: underline
  text-transform: uppercase

#menu > div:hover
  background-color: #DEDEDE

#menu > div.selected
  color: white
  background-color: #3BB30B

#logo
  font-size: 1.5em

</style>
