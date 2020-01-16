<template lang="html">
<div class="">
  <input type="text" name="" v-model="typedCountry">
  <select v-model="selection">
    <!-- <option disabled value="">Please select one</option> -->
    <!-- it has to be set as default when is selected -->
    <option v-for="(country, index) in countries" :key='index' :value="country" >{{ country.name }}</option>
  </select>
</div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: "country-selector",
  props: ['countries'],
  data() {
    return {
      selection: null,
      typedCountry: ""
    }
  },
  watch: {
    searchCountry(value) {
      this.selection = value;
      eventBus.$emit('country-selected', value);
    },
    selection(value) {
      eventBus.$emit('country-selected', value);
    }
  },
  // methods: {
  computed: {
    // emitFromSelection() {
    //   eventBus.$emit('country-selected', this.selection)
    // },

    searchCountry() {
      const countriesMapped = this.countries.map(country => country.name)
      const startWithName = countriesMapped.find(countryName => countryName.toLowerCase().startsWith(this.typedCountry.toLowerCase()))
      const findObjCountry = this.countries.find(country => country.name === startWithName)
      // computed should never assign
      // this.selection = findObjCountry
      return findObjCountry
    },

    }
  }

</script>

<style lang="css" scoped>
</style>
