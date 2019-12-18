<template>
  <div id="app">
    <country-list :countries="countries"/>
    <country-list-item/>
    <country-details :country="selectedCountry"/>
  </div>
</template>

<script>
import {eventBus} from "./main.js";
import CountryList from "./components/countryList.vue";
import CountryItem from "./components/countryListItem.vue";
import CountryDetails from "./components/countryDetails.vue";


export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null
    }
  },

  mounted(){
    this.getCountries();
    eventBus.$on("select-country", (country) => {
      this.selectedCountry = country
    })
  },

  methods: {
    getCountries(){
      const request = fetch("https://restcountries.eu/rest/v2/all")
      .then(response => response.json())
      .then((data) => {
        this.countries = data;
      });
    }
  },

  components: {
    "country-list" : CountryList,
    "country-list-item": CountryItem,
    "country-details": CountryDetails
  }
}
</script>

<style>

</style>
