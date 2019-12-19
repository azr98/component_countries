<template lang="html">
  <input v-on:input="handleInput" placeholder="search country..."  type="text" v-model="filterInput">
</template>

<script>

import {eventBus} from "../main.js";

export default {
  name: "country-filter",
  props: [],
  data(){
    return {
      filterInput: ""
    }
  },
  methods:{
    handleInput(){
      eventBus.$emit("filter-country", this.filterInput)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
