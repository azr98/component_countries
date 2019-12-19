<template lang="html">
  <div class="">
    <label for="country-select">Select Country</label>
    <select id="country-select"v-model="country" v-on:change="handleChange">
      <option v-for="country in countries" :value = "country">{{country.name}}</option>
    </select>
  </div>
</template>

<script>

import {eventBus} from "../main.js";

export default {
  name: "country-option",
  props: ['countries'],
  data(){
    return{
      country: null
    }
  },
  methods: {
    handleChange(){
      eventBus.$emit("change-country", this.country);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
