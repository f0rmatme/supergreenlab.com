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
  <section :id='$style.container'>
    <div :id='$style.title'>
      <SectionTitle title='Our bundles are'
                    green='all included'
                    separator='true'/>
    </div>
    <div :id='$style.steps'>
      <div :class='$style.step'>
        <Step n=1
              title='Top of the line LEDs'
              text='Providing optimal lighting and little heat. Perfect for the <b>whole life cycle</b> of your grow. The LEDs produce very little heat, perfect for stealth growths.' 
              icon='light.svg' />
      </div>
      <div :class='$style.step'>
        <Step n=2
              title='Ventilation'
              text='All our kits <b>come with ventilation</b>, which ensures <b>heat and humidity</b> control, aswell as <b>odor filtering</b>.'
              icon='ventilation.svg' />
      </div>
      <div :class='$style.step'>
        <Step n=3
              title='Sensors'
              text="Kits are included with an <b>humidity and temperature sensor.</b> Keep an eye on your grow even when <b>you're not at home!</b>"
              icon='sensor.svg' />
      </div>
      <div :class='$style.step'>
        <Step n=4
              title='Free app'
              text='<b>Fine-tuning, monitoring and having a live view on your grow</b>, all from your <b>phone!</b> The app also includes tips and tricks to ensure the <b>best yield<b> from your grow!'
              icon='app.svg' />
      </div>
    </div>
  </section>
</template>

<script>
import SectionTitle from '~/components/sectiontitle.vue'
import Step from '~/components/homesection-step.vue'

export default {
  components: { SectionTitle, Step, },
}

</script>

<style module lang=stylus>

#container
  display: flex
  width: 100%
  flex-direction: column
  justify-content: center
  align-items: center

#steps
  display: flex
  align-items: center
  justify-content: space-around
  flex-wrap: wrap
  margin: 20pt 0 40pt 0

.step
  flex-basis: 40%
  margin-top: 20pt

#title
  width: 100%

</style>
