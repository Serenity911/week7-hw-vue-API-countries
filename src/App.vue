<template>
  <div>
    <country-selector :countries='countries'> </country-selector>
    <div>
      <country-details v-if='selectedCountry' :country='selectedCountry'> </country-details>
      <!-- <p v-if='selectedCountry'>{{ selectedCountry.name }}</p> -->
    </div>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import CountrySelector from './components/countrySelector.vue'
import CountryDetails from './components/countryDetails.vue'

export default {
  name: 'app',
  data() {
    return {
      countries: [],
      selectedCountry: null
    }
  },
  mounted() {
    this.fetchCountries()
    eventBus.$on('country-selected', (selection) => { this.selectedCountry = selection})
  },
  methods: {
    fetchCountries: function () {
        fetch('https://restcountries.eu/rest/v2/all')
        .then(result => result.json())
        .then(countries => this.countries = countries)
    }
  },
  components: {
    "country-selector": CountrySelector,
    "country-details": CountryDetails
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
