<template lang="html">
<div class="">
  <input type="text" name="" v-model="typedCountry">
  <select v-model="selection">
    <!-- <option disabled value="">Please select one</option> -->
    <option v-for="(country, index) in countries" :key='index' :value="country" >{{ country.name }}</option>
  </select>
</div>
</template>

<script>
export default {
  name: "country-selector",
  props: ['countries'],
  data() {
    return {
      selection: null,
      typedCountry: null
    }
  },
  computed: {
    logSelection() {
      // console.log(this.selection);
      return this.selection;
    },
    searchCountry() {
      // console.log(this.typedCountry);
      let countriesMapped = this.countries.map(country => country.name)
      // console.log(countriesMapped);
      let startWithName = countriesMapped.find(countryName => countryName.toLowerCase().startsWith(this.typedCountry.toLowerCase()))
      return this.selection = startWithName
      // console.log(startWithName);
      }
    }
  }

</script>

<style lang="css" scoped>
</style>
