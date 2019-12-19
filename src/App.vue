<template>
  <div id="app">
    <country-select :countries = "countries"/>
    <country-details :country="selectedCountry"/>
    <country-filter/>
    <country-list :countries="countriesFiltered"/>
  </div>
</template>

<script>
import {eventBus} from "./main.js";
import CountryList from "./components/countryList.vue";
import CountryItem from "./components/countryListItem.vue";
import CountryDetails from "./components/countryDetails.vue";
import CountrySelect from "./components/countrySelect.vue";
import CountryFilter from "./components/countryFilter.vue"

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      countriesFiltered: [],
      selectedCountry: null
    }
  },

  mounted(){
    this.getCountries();
    eventBus.$on("select-country", (country) => {
      this.selectedCountry = country
    });

    eventBus.$on("change-country", (country) => {
      this.selectedCountry = country;
    })

    eventBus.$on("filter-country", (filterInput) => {

      this.countries.forEach((country) => {
        if(filterInput.length > 0){
          if(country.name.toLowerCase().indexOf(filterInput) !== -1){
            this.selectedCountry = country;
          }
        }
      })

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
    "country-details": CountryDetails,
    "country-select": CountrySelect,
    "country-filter": CountryFilter
  }
}
</script>

<style>

</style>
